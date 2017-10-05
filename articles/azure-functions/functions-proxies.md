---
title: Werken met proxy's in Azure Functions | Microsoft Docs
description: Overzicht van het gebruik van Azure Functions-proxy 's
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
ms.openlocfilehash: 102e54627a8fee721d3ed85e86a8009e706bb5b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="44c81-103">Werken met Azure Functions-proxy's (preview)</span><span class="sxs-lookup"><span data-stu-id="44c81-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="44c81-104">Azure Functions-proxy's is momenteel in preview.</span><span class="sxs-lookup"><span data-stu-id="44c81-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="44c81-105">Het is gratis terwijl in preview, maar standaardfuncties facturering is van toepassing op de proxy-uitvoeringen.</span><span class="sxs-lookup"><span data-stu-id="44c81-105">It is free while in preview, but standard Functions billing applies to proxy executions.</span></span> <span data-ttu-id="44c81-106">Zie voor meer informatie [prijzen van Azure Functions](https://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="44c81-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="44c81-107">In dit artikel wordt uitgelegd hoe configureren en werken met Azure Functions-proxy's.</span><span class="sxs-lookup"><span data-stu-id="44c81-107">This article explains how to configure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="44c81-108">Met deze functie kunt u eindpunten op de functie-app die zijn geïmplementeerd door een andere resource.</span><span class="sxs-lookup"><span data-stu-id="44c81-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="44c81-109">U kunt deze proxy's gebruiken om een grote API in meerdere functie-apps (zoals in een microservice-architectuur), terwijl u nog steeds één API-gebied voor clients.</span><span class="sxs-lookup"><span data-stu-id="44c81-109">You can use these proxies to break a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="44c81-110"><a name="enable"></a>Azure Functions-proxy's inschakelen</span><span class="sxs-lookup"><span data-stu-id="44c81-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="44c81-111">Proxy's worden niet standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="44c81-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="44c81-112">U kunt proxy's kunt maken, terwijl de functie is uitgeschakeld, maar ze niet kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="44c81-112">You can create proxies while the feature is disabled, but they will not execute.</span></span> <span data-ttu-id="44c81-113">Als u wilt inschakelen op proxy's, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="44c81-113">To enable proxies, do the following:</span></span>

1. <span data-ttu-id="44c81-114">Open de [Azure-portal], en gaat u naar de functie-app.</span><span class="sxs-lookup"><span data-stu-id="44c81-114">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="44c81-115">Selecteer **werken app-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="44c81-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="44c81-116">Switch **inschakelen Azure Functions-proxy's (preview)** naar **op**.</span><span class="sxs-lookup"><span data-stu-id="44c81-116">Switch **Enable Azure Functions Proxies (preview)** to **On**.</span></span>

<span data-ttu-id="44c81-117">U kunt ook hier retourneren voor het bijwerken van de proxy-runtime, nieuwe functies beschikbaar komen.</span><span class="sxs-lookup"><span data-stu-id="44c81-117">You can also return here to update the proxy runtime as new features become available.</span></span>


## <span data-ttu-id="44c81-118"><a name="create"></a>Maken van een proxy</span><span class="sxs-lookup"><span data-stu-id="44c81-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="44c81-119">Deze sectie wordt beschreven hoe u een proxy in de portal functies maken.</span><span class="sxs-lookup"><span data-stu-id="44c81-119">This section shows you how to create a proxy in the Functions portal.</span></span>

1. <span data-ttu-id="44c81-120">Open de [Azure-portal], en gaat u naar de functie-app.</span><span class="sxs-lookup"><span data-stu-id="44c81-120">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="44c81-121">Selecteer in het linkerdeelvenster **nieuwe proxy**.</span><span class="sxs-lookup"><span data-stu-id="44c81-121">In the left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="44c81-122">Geef een naam voor de proxy.</span><span class="sxs-lookup"><span data-stu-id="44c81-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="44c81-123">Het eindpunt dat wordt weergegeven op deze functie-app configureren door te geven de **Routesjabloon** en **HTTP-methoden**.</span><span class="sxs-lookup"><span data-stu-id="44c81-123">Configure the endpoint that's exposed on this function app by specifying the **route template** and **HTTP methods**.</span></span> <span data-ttu-id="44c81-124">Deze parameters zich gedragen volgens de regels voor [HTTP-triggers].</span><span class="sxs-lookup"><span data-stu-id="44c81-124">These parameters behave according to the rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="44c81-125">Stel de **back-end-URL** naar een ander eindpunt.</span><span class="sxs-lookup"><span data-stu-id="44c81-125">Set the **backend URL** to another endpoint.</span></span> <span data-ttu-id="44c81-126">Dit eindpunt kan een functie in een andere functie-app, of andere API kan zijn.</span><span class="sxs-lookup"><span data-stu-id="44c81-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="44c81-127">De waarde niet hoeft te worden statische en deze kan verwijzen naar [toepassingsinstellingen] en [parameters van de aanvraag van de oorspronkelijke client].</span><span class="sxs-lookup"><span data-stu-id="44c81-127">The value does not need to be static, and it can reference [application settings] and [parameters from the original client request].</span></span>
6. <span data-ttu-id="44c81-128">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="44c81-128">Click **Create**.</span></span>

<span data-ttu-id="44c81-129">De proxy bestaat nu als een nieuw eindpunt op functie-app.</span><span class="sxs-lookup"><span data-stu-id="44c81-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="44c81-130">Vanuit het clientperspectief van een is het equivalent zijn aan een HttpTrigger in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="44c81-130">From a client perspective, it is equivalent to an HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="44c81-131">U kunt uw nieuwe proxy uitproberen door te kopiëren van de Proxy-URL en testen van het met uw favoriete HTTP-client.</span><span class="sxs-lookup"><span data-stu-id="44c81-131">You can try out your new proxy by copying the Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="44c81-132"><a name="modify-requests-responses"></a>Aanvragen en antwoorden wijzigen</span><span class="sxs-lookup"><span data-stu-id="44c81-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="44c81-133">U kunt met Azure Functions-proxy's, aanvragen en antwoorden van de back-end wijzigen.</span><span class="sxs-lookup"><span data-stu-id="44c81-133">With Azure Functions Proxies, you can modify requests to and responses from the back end.</span></span> <span data-ttu-id="44c81-134">Deze transformaties kunnen variabelen gebruiken zoals gedefinieerd in [variabelen gebruiken].</span><span class="sxs-lookup"><span data-stu-id="44c81-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="44c81-135"><a name="modify-backend-request"></a>De back-end-aanvraag wijzigen</span><span class="sxs-lookup"><span data-stu-id="44c81-135"><a name="modify-backend-request"></a>Modify the back-end request</span></span>

<span data-ttu-id="44c81-136">Standaard wordt de back-end-aanvraag geïnitialiseerd als een kopie van de oorspronkelijke aanvraag.</span><span class="sxs-lookup"><span data-stu-id="44c81-136">By default, the back-end request is initialized as a copy of the original request.</span></span> <span data-ttu-id="44c81-137">Naast het instellen van de back-end-URL, kunt u wijzigingen aanbrengt aan de HTTP-methode, kopteksten en queryreeksparameters.</span><span class="sxs-lookup"><span data-stu-id="44c81-137">In addition to setting the back-end URL, you can make changes to the HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="44c81-138">De gewijzigde waarden kunnen verwijzen naar [toepassingsinstellingen] en [parameters van de aanvraag van de oorspronkelijke client].</span><span class="sxs-lookup"><span data-stu-id="44c81-138">The modified values can reference [application settings] and [parameters from the original client request].</span></span>

<span data-ttu-id="44c81-139">Er is momenteel geen portal ervaring voor het wijzigen van de back-end-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="44c81-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="44c81-140">Zie voor meer informatie over het toepassen van deze mogelijkheid van proxies.json, [definiëren van een object requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="44c81-140">To learn how to apply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="44c81-141"><a name="modify-response"></a>Het antwoord worden gewijzigd</span><span class="sxs-lookup"><span data-stu-id="44c81-141"><a name="modify-response"></a>Modify the response</span></span>

<span data-ttu-id="44c81-142">Het antwoord van de client wordt standaard geïnitialiseerd als een kopie van het back-end-antwoord.</span><span class="sxs-lookup"><span data-stu-id="44c81-142">By default, the client response is initialized as a copy of the back-end response.</span></span> <span data-ttu-id="44c81-143">U kunt wijzigingen aanbrengen statuscode, reden, kopteksten en hoofdtekst van het antwoord.</span><span class="sxs-lookup"><span data-stu-id="44c81-143">You can make changes to the response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="44c81-144">De gewijzigde waarden kunnen verwijzen naar [toepassingsinstellingen], [parameters van de aanvraag van de oorspronkelijke client], en [parameters uit het antwoord van de back-end].</span><span class="sxs-lookup"><span data-stu-id="44c81-144">The modified values can reference [application settings], [parameters from the original client request], and [parameters from the back-end response].</span></span>

<span data-ttu-id="44c81-145">Er is momenteel geen portal ervaring voor het wijzigen van antwoorden.</span><span class="sxs-lookup"><span data-stu-id="44c81-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="44c81-146">Zie voor meer informatie over het toepassen van deze mogelijkheid van proxies.json, [definiëren van een object responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="44c81-146">To learn how to apply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="44c81-147"><a name="using-variables"></a>Variabelen gebruiken</span><span class="sxs-lookup"><span data-stu-id="44c81-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="44c81-148">De configuratie voor een proxy hoeft niet statisch.</span><span class="sxs-lookup"><span data-stu-id="44c81-148">The configuration for a proxy does not need to be static.</span></span> <span data-ttu-id="44c81-149">U kunt het gebruik van variabelen in de oorspronkelijke aanvraag, back-end antwoord of toepassingsinstellingen voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="44c81-149">You can condition it to use variables from the original request, the back-end response, or application settings.</span></span>

### <span data-ttu-id="44c81-150"><a name="request-parameters"></a>Aanvraagparameters verwijzing</span><span class="sxs-lookup"><span data-stu-id="44c81-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="44c81-151">U kunt de aanvraagparameters gebruiken als invoer voor de eigenschap van de back-end-URL of als onderdeel van het wijzigen van aanvragen en antwoorden.</span><span class="sxs-lookup"><span data-stu-id="44c81-151">You can use request parameters as inputs to the back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="44c81-152">Sommige parameters kunnen afhankelijk zijn van de Routesjabloon die opgegeven in de base proxyconfiguratie en anderen kunnen afkomstig zijn uit de eigenschappen van de binnenkomende aanvraag.</span><span class="sxs-lookup"><span data-stu-id="44c81-152">Some parameters can be bound from the route template that's specified in the base proxy configuration, and others can come from properties of the incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="44c81-153">Route-Sjabloonparameters</span><span class="sxs-lookup"><span data-stu-id="44c81-153">Route template parameters</span></span>
<span data-ttu-id="44c81-154">Parameters die worden gebruikt in de Routesjabloon zijn beschikbaar voor worden verwezen met de naam.</span><span class="sxs-lookup"><span data-stu-id="44c81-154">Parameters that are used in the route template are available to be referenced by name.</span></span> <span data-ttu-id="44c81-155">De parameternamen moeten tussen accolades ({}).</span><span class="sxs-lookup"><span data-stu-id="44c81-155">The parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="44c81-156">Bijvoorbeeld, als een proxy heeft een Routesjabloon zoals `/pets/{petId}`, de URL van de back-end kan de waarde van bevatten `{petId}`als in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span><span class="sxs-lookup"><span data-stu-id="44c81-156">For example, if a proxy has a route template, such as `/pets/{petId}`, the back-end URL can include the value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="44c81-157">Als het Routesjabloon wordt beëindigd in een jokerteken, zoals `/api/{*restOfPath}`, de waarde `{restOfPath}` is een tekenreeksrepresentatie van de resterende padsegmenten van de binnenkomende aanvraag.</span><span class="sxs-lookup"><span data-stu-id="44c81-157">If the route template terminates in a wildcard, such as `/api/{*restOfPath}`, the value `{restOfPath}` is a string representation of the remaining path segments from the incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="44c81-158">Aanvullende aanvraagparameters</span><span class="sxs-lookup"><span data-stu-id="44c81-158">Additional request parameters</span></span>
<span data-ttu-id="44c81-159">Naast de sjabloonparameters route kunnen configuratiewaarden in de volgende waarden worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="44c81-159">In addition to the route template parameters, the following values can be used in config values:</span></span>

* <span data-ttu-id="44c81-160">**{request.method}** : De HTTP-methode die wordt gebruikt op de oorspronkelijke aanvraag.</span><span class="sxs-lookup"><span data-stu-id="44c81-160">**{request.method}**: The HTTP method that's used on the original request.</span></span>
* <span data-ttu-id="44c81-161">**{request.headers. \<HeaderName is opgeslagen\>}**: een header die kan worden gelezen vanaf de oorspronkelijke aanvraag.</span><span class="sxs-lookup"><span data-stu-id="44c81-161">**{request.headers.\<HeaderName\>}**: A header that can be read from the original request.</span></span> <span data-ttu-id="44c81-162">Vervang  *\<HeaderName is opgeslagen\>*  met de naam van de header die u wilt lezen.</span><span class="sxs-lookup"><span data-stu-id="44c81-162">Replace *\<HeaderName\>* with the name of the header that you want to read.</span></span> <span data-ttu-id="44c81-163">Als de header niet in de aanvraag opgenomen is, wordt de waarde een lege tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="44c81-163">If the header is not included on the request, the value will be the empty string.</span></span>
* <span data-ttu-id="44c81-164">**{request.querystring. \<ParameterName\>}**: een queryreeksparameter opgeven die kan worden gelezen vanaf de oorspronkelijke aanvraag.</span><span class="sxs-lookup"><span data-stu-id="44c81-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from the original request.</span></span> <span data-ttu-id="44c81-165">Vervang  *\<ParameterName\>*  met de naam van de parameter die u wilt lezen.</span><span class="sxs-lookup"><span data-stu-id="44c81-165">Replace *\<ParameterName\>* with the name of the parameter that you want to read.</span></span> <span data-ttu-id="44c81-166">Als de parameter niet in de aanvraag opgenomen is, wordt de waarde een lege tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="44c81-166">If the parameter is not included on the request, the value will be the empty string.</span></span>

### <span data-ttu-id="44c81-167"><a name="response-parameters"></a>Verwijzing naar back-end antwoord parameters</span><span class="sxs-lookup"><span data-stu-id="44c81-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="44c81-168">Antwoord parameters kunnen worden gebruikt als onderdeel van het wijzigen van het antwoord op de client.</span><span class="sxs-lookup"><span data-stu-id="44c81-168">Response parameters can be used as part of modifying the response to the client.</span></span> <span data-ttu-id="44c81-169">De volgende waarden kunnen worden gebruikt in configuratiewaarden:</span><span class="sxs-lookup"><span data-stu-id="44c81-169">The following values can be used in config values:</span></span>

* <span data-ttu-id="44c81-170">**{backend.response.statusCode}** : De HTTP-statuscode die op de back-end-antwoord wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="44c81-170">**{backend.response.statusCode}**: The HTTP status code that's returned on the back-end response.</span></span>
* <span data-ttu-id="44c81-171">**{backend.response.statusReason}** : De HTTP-reden dat wordt geretourneerd van het back-end-antwoord.</span><span class="sxs-lookup"><span data-stu-id="44c81-171">**{backend.response.statusReason}**: The HTTP reason phrase that's returned on the back-end response.</span></span>
* <span data-ttu-id="44c81-172">**{backend.response.headers. \<HeaderName is opgeslagen\>}**: een koptekst die kan worden gelezen uit het antwoord van de back-end.</span><span class="sxs-lookup"><span data-stu-id="44c81-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from the back-end response.</span></span> <span data-ttu-id="44c81-173">Vervang  *\<HeaderName is opgeslagen\>*  met de naam van de header die u wilt lezen.</span><span class="sxs-lookup"><span data-stu-id="44c81-173">Replace *\<HeaderName\>* with the name of the header you want to read.</span></span> <span data-ttu-id="44c81-174">Als de header niet in de aanvraag opgenomen is, wordt de waarde een lege tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="44c81-174">If the header is not included on the request, the value will be the empty string.</span></span>

### <span data-ttu-id="44c81-175"><a name="use-appsettings"></a>Toepassingsinstellingen-verwijzing</span><span class="sxs-lookup"><span data-stu-id="44c81-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="44c81-176">U kunt ook verwijzen naar [toepassingsinstellingen gedefinieerd voor de functie-app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) door de naam van de instelling tussen procenttekens (%).</span><span class="sxs-lookup"><span data-stu-id="44c81-176">You can also reference [application settings defined for the function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding the setting name with percent signs (%).</span></span>

<span data-ttu-id="44c81-177">Bijvoorbeeld, een back-end-URL van *https://%ORDER_PROCESSING_HOST%/api/orders* "% ORDER_PROCESSING_HOST %" vervangen door de waarde van de instelling ORDER_PROCESSING_HOST zou hebben.</span><span class="sxs-lookup"><span data-stu-id="44c81-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with the value of the ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="44c81-178">Toepassingsinstellingen voor back-end-hosts gebruiken wanneer u meerdere implementaties of testomgeving.</span><span class="sxs-lookup"><span data-stu-id="44c81-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="44c81-179">Op die manier kunt u ervoor zorgen dat u altijd communiceren met de juiste back-end voor deze omgeving communiceren.</span><span class="sxs-lookup"><span data-stu-id="44c81-179">That way, you can make sure that you are always talking to the right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="44c81-180">Geavanceerde configuratie</span><span class="sxs-lookup"><span data-stu-id="44c81-180">Advanced configuration</span></span>

<span data-ttu-id="44c81-181">De proxy's die u configureert, worden opgeslagen in een bestand proxies.json, dat in de hoofdmap van een functie app-map bevindt zich.</span><span class="sxs-lookup"><span data-stu-id="44c81-181">The proxies that you configure are stored in a proxies.json file, which is located in the root of a function app directory.</span></span> <span data-ttu-id="44c81-182">U kunt handmatig bewerken van dit bestand en implementeren als onderdeel van uw app als u een van de [implementatiemethoden](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) die functies worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="44c81-182">You can manually edit this file and deploy it as part of your app when you use any of the [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="44c81-183">De functie moet [ingeschakeld](#enable) het bestand moet worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="44c81-183">The feature must be [enabled](#enable) for the file to be processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="44c81-184">Als u geen hebt ingesteld een van de methoden voor het implementeren, kunt u ook werken met het bestand proxies.json in de portal.</span><span class="sxs-lookup"><span data-stu-id="44c81-184">If you have not set up one of the deployment methods, you can also work with the proxies.json file in the portal.</span></span> <span data-ttu-id="44c81-185">Ga naar de functie-app, selecteer **platformfuncties**, en selecteer vervolgens **App Service-Editor**.</span><span class="sxs-lookup"><span data-stu-id="44c81-185">Go to your function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="44c81-186">Door dit te doen, kunt u de volledige structuur van uw app functie weergeven en brengt wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="44c81-186">By doing so, you can view the entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="44c81-187">Proxies.JSON wordt gedefinieerd door een object proxy's, die bestaan uit benoemde proxy's en de bijbehorende definities.</span><span class="sxs-lookup"><span data-stu-id="44c81-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="44c81-188">Eventueel, als uw editor ondersteunt, kunt u verwijzen naar een [JSON-schema](http://json.schemastore.org/proxies) voor de codevoltooiing.</span><span class="sxs-lookup"><span data-stu-id="44c81-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="44c81-189">Een voorbeeld van een bestand kan er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="44c81-189">An example file might look like the following:</span></span>

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

<span data-ttu-id="44c81-190">Elke proxy heeft een beschrijvende naam, zoals *proxy1* in het voorgaande voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="44c81-190">Each proxy has a friendly name, such as *proxy1* in the preceding example.</span></span> <span data-ttu-id="44c81-191">Het bijbehorende proxy definitie van object wordt gedefinieerd door de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="44c81-191">The corresponding proxy definition object is defined by the following properties:</span></span>

* <span data-ttu-id="44c81-192">**matchCondition**: vereist--een object voor het definiëren van de aanvragen die de uitvoering van deze proxy activeren.</span><span class="sxs-lookup"><span data-stu-id="44c81-192">**matchCondition**: Required--an object defining the requests that trigger the execution of this proxy.</span></span> <span data-ttu-id="44c81-193">Deze twee eigenschappen die worden gedeeld met bevat [HTTP-triggers]:</span><span class="sxs-lookup"><span data-stu-id="44c81-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="44c81-194">_methoden_: een matrix van de HTTP-methoden die de proxy reageert op.</span><span class="sxs-lookup"><span data-stu-id="44c81-194">_methods_: An array of the HTTP methods that the proxy responds to.</span></span> <span data-ttu-id="44c81-195">Als deze niet is opgegeven, wordt de proxy reageert op HTTP-methoden worden op de route.</span><span class="sxs-lookup"><span data-stu-id="44c81-195">If it is not specified, the proxy responds to all HTTP methods on the route.</span></span>
    * <span data-ttu-id="44c81-196">_route_: vereist--definieert het Routesjabloon beheren die aanvragen URL's van uw proxy reageert op.</span><span class="sxs-lookup"><span data-stu-id="44c81-196">_route_: Required--defines the route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="44c81-197">In tegenstelling tot in de HTTP-triggers is er geen standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="44c81-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="44c81-198">**backendUri**: de URL van de back-end-resource waarnaar de aanvraag via proxy moet.</span><span class="sxs-lookup"><span data-stu-id="44c81-198">**backendUri**: The URL of the back-end resource to which the request should be proxied.</span></span> <span data-ttu-id="44c81-199">Deze waarde kan verwijzen naar toepassingsinstellingen en parameters van de aanvraag van de oorspronkelijke client.</span><span class="sxs-lookup"><span data-stu-id="44c81-199">This value can reference application settings and parameters from the original client request.</span></span> <span data-ttu-id="44c81-200">Als deze eigenschap niet opgenomen is, wordt Azure Functions reageert met een HTTP 200 OK.</span><span class="sxs-lookup"><span data-stu-id="44c81-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="44c81-201">**requestOverrides**: een object dat transformaties de back-end-aanvraag bepaalt.</span><span class="sxs-lookup"><span data-stu-id="44c81-201">**requestOverrides**: An object that defines transformations to the back-end request.</span></span> <span data-ttu-id="44c81-202">Zie [definiëren van een object requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="44c81-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="44c81-203">**responseOverrides**: een object dat transformaties aan de reactie van de client bepaalt.</span><span class="sxs-lookup"><span data-stu-id="44c81-203">**responseOverrides**: An object that defines transformations to the client response.</span></span> <span data-ttu-id="44c81-204">Zie [definiëren van een object responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="44c81-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="44c81-205">De eigenschap route Azure Functions-proxy's worden niet door de eigenschap routePrefix van de host-configuratie van functies.</span><span class="sxs-lookup"><span data-stu-id="44c81-205">The route property Azure Functions Proxies does not honor the routePrefix property of the Functions host configuration.</span></span> <span data-ttu-id="44c81-206">Als u opnemen een voorvoegsel zoals /api wilt, moet worden opgenomen in de route-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="44c81-206">If you want to include a prefix such as /api, it must be included in the route property.</span></span>

### <span data-ttu-id="44c81-207"><a name="requestOverrides"></a>Een object requestOverrides definiëren</span><span class="sxs-lookup"><span data-stu-id="44c81-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="44c81-208">Het object requestOverrides definieert wijzigingen aangebracht aan de aanvraag toen de back-end-bron wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="44c81-208">The requestOverrides object defines changes made to the request when the back-end resource is called.</span></span> <span data-ttu-id="44c81-209">Het object wordt gedefinieerd door de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="44c81-209">The object is defined by the following properties:</span></span>

* <span data-ttu-id="44c81-210">**backend.Request.Method**: de HTTP-methode die wordt gebruikt voor het aanroepen van de back-end.</span><span class="sxs-lookup"><span data-stu-id="44c81-210">**backend.request.method**: The HTTP method that's used to call the back end.</span></span>
* <span data-ttu-id="44c81-211">**backend.Request.QueryString. \<ParameterName\>**: een queryreeksparameter opgeven die kan worden ingesteld voor het aanroepen van de back-end.</span><span class="sxs-lookup"><span data-stu-id="44c81-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for the call to the back end.</span></span> <span data-ttu-id="44c81-212">Vervang  *\<ParameterName\>*  met de naam van de parameter die u wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="44c81-212">Replace *\<ParameterName\>* with the name of the parameter that you want to set.</span></span> <span data-ttu-id="44c81-213">Als de lege tekenreeks is opgegeven, wordt de parameter niet opgenomen in de back-end-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="44c81-213">If the empty string is provided, the parameter is not included on the back-end request.</span></span>
* <span data-ttu-id="44c81-214">**backend.Request.headers. \<HeaderName is opgeslagen\>**: een header die kan worden ingesteld voor het aanroepen van de back-end.</span><span class="sxs-lookup"><span data-stu-id="44c81-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for the call to the back end.</span></span> <span data-ttu-id="44c81-215">Vervang  *\<HeaderName is opgeslagen\>*  met de naam van de header die u wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="44c81-215">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="44c81-216">Als u een lege tekenreeks opgeeft, wordt de koptekst niet opgenomen in de back-end-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="44c81-216">If you provide the empty string, the header is not included on the back-end request.</span></span>

<span data-ttu-id="44c81-217">Waarden kunnen verwijzen naar toepassingsinstellingen en parameters van de aanvraag van de oorspronkelijke client.</span><span class="sxs-lookup"><span data-stu-id="44c81-217">Values can reference application settings and parameters from the original client request.</span></span>

<span data-ttu-id="44c81-218">Een voorbeeldconfiguratie kan er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="44c81-218">An example configuration might look like the following:</span></span>

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

### <span data-ttu-id="44c81-219"><a name="responseOverrides"></a>Een object responseOverrides definiëren</span><span class="sxs-lookup"><span data-stu-id="44c81-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="44c81-220">Het object requestOverrides definieert wijzigingen die zijn aangebracht aan de reactie die wordt doorgegeven aan de client.</span><span class="sxs-lookup"><span data-stu-id="44c81-220">The requestOverrides object defines changes that are made to the response that's passed back to the client.</span></span> <span data-ttu-id="44c81-221">Het object wordt gedefinieerd door de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="44c81-221">The object is defined by the following properties:</span></span>

* <span data-ttu-id="44c81-222">**response.statusCode**: de HTTP-statuscode moet worden geretourneerd naar de client.</span><span class="sxs-lookup"><span data-stu-id="44c81-222">**response.statusCode**: The HTTP status code to be returned to the client.</span></span>
* <span data-ttu-id="44c81-223">**response.statusReason**: de HTTP-reden wordt geretourneerd naar de client.</span><span class="sxs-lookup"><span data-stu-id="44c81-223">**response.statusReason**: The HTTP reason phrase to be returned to the client.</span></span>
* <span data-ttu-id="44c81-224">**Response.BODY**: de tekenreeksrepresentatie van de instantie moet worden geretourneerd naar de client.</span><span class="sxs-lookup"><span data-stu-id="44c81-224">**response.body**: The string representation of the body to be returned to the client.</span></span>
* <span data-ttu-id="44c81-225">**Response.headers. \<HeaderName is opgeslagen\>**: een header die kan worden ingesteld voor het antwoord op de client.</span><span class="sxs-lookup"><span data-stu-id="44c81-225">**response.headers.\<HeaderName\>**: A header that can be set for the response to the client.</span></span> <span data-ttu-id="44c81-226">Vervang  *\<HeaderName is opgeslagen\>*  met de naam van de header die u wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="44c81-226">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="44c81-227">Als u een lege tekenreeks opgeeft, wordt de koptekst niet opgenomen in het antwoord.</span><span class="sxs-lookup"><span data-stu-id="44c81-227">If you provide the empty string, the header is not included on the response.</span></span>

<span data-ttu-id="44c81-228">Waarden kunnen verwijzen naar toepassingsinstellingen, de parameters van de aanvraag van de oorspronkelijke client en de parameters van het back-end-antwoord.</span><span class="sxs-lookup"><span data-stu-id="44c81-228">Values can reference application settings, parameters from the original client request, and parameters from the back-end response.</span></span>

<span data-ttu-id="44c81-229">Een voorbeeldconfiguratie kan er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="44c81-229">An example configuration might look like the following:</span></span>

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
> <span data-ttu-id="44c81-230">In dit voorbeeld wordt de instantie wordt ingesteld rechtstreeks, dus er is geen `backendUri` eigenschap nodig is.</span><span class="sxs-lookup"><span data-stu-id="44c81-230">In this example, the body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="44c81-231">Het voorbeeld ziet hoe u Azure Functions-proxy's kunt gebruiken voor mocking API's.</span><span class="sxs-lookup"><span data-stu-id="44c81-231">The example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

<span data-ttu-id="44c81-232">[Azure-portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="44c81-232">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="44c81-233">[HTTP-triggers]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger</span><span class="sxs-lookup"><span data-stu-id="44c81-233">[HTTP triggers]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger</span></span>
[Modify the back-end request]: #modify-backend-request
[Modify the response]: #modify-response
<span data-ttu-id="44c81-234">[definiëren van een object requestOverrides]: #requestOverrides</span><span class="sxs-lookup"><span data-stu-id="44c81-234">[Define a requestOverrides object]: #requestOverrides</span></span>
<span data-ttu-id="44c81-235">[definiëren van een object responseOverrides]: #responseOverrides</span><span class="sxs-lookup"><span data-stu-id="44c81-235">[Define a responseOverrides object]: #responseOverrides</span></span>
<span data-ttu-id="44c81-236">[toepassingsinstellingen]: #use-appsettings</span><span class="sxs-lookup"><span data-stu-id="44c81-236">[application settings]: #use-appsettings</span></span>
<span data-ttu-id="44c81-237">[variabelen gebruiken]: #using-variables</span><span class="sxs-lookup"><span data-stu-id="44c81-237">[Use variables]: #using-variables</span></span>
<span data-ttu-id="44c81-238">[parameters van de aanvraag van de oorspronkelijke client]: #request-parameters</span><span class="sxs-lookup"><span data-stu-id="44c81-238">[parameters from the original client request]: #request-parameters</span></span>
<span data-ttu-id="44c81-239">[parameters uit het antwoord van de back-end]: #response-parameters</span><span class="sxs-lookup"><span data-stu-id="44c81-239">[parameters from the back-end response]: #response-parameters</span></span>
