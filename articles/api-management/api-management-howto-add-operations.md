---
title: aaaHow tooadd operations tooan API in Azure API Management | Microsoft Docs
description: Meer informatie over hoe tooadd operations tooan API in Azure API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d57fa59a2b0ceb392cde23150a0cbb326e52d27d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-operations-tooan-api-in-azure-api-management"></a><span data-ttu-id="44319-103">Hoe tooadd operations tooan API in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="44319-103">How tooadd operations tooan API in Azure API Management</span></span>
<span data-ttu-id="44319-104">Voordat een API in API Management kan worden gebruikt, kunnen bewerkingen moeten worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="44319-104">Before an API in API Management can be used, operations must be added.</span></span> <span data-ttu-id="44319-105">Dit toont hoe begeleiden tooadd en configureren van verschillende soorten bewerkingen tooan API in API Management.</span><span class="sxs-lookup"><span data-stu-id="44319-105">This guide shows how tooadd and configure different types of operations tooan API in API Management.</span></span>

## <span data-ttu-id="44319-106"><a name="add-operation"></a>Een bewerking toevoegen</span><span class="sxs-lookup"><span data-stu-id="44319-106"><a name="add-operation"> </a>Add an operation</span></span>
<span data-ttu-id="44319-107">Bewerkingen worden toegevoegd en tooan API in de publicatieportal Hallo geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="44319-107">Operations are added and configured tooan API in hello publisher portal.</span></span> <span data-ttu-id="44319-108">tooaccess publisher en klik op Hallo **publicatieportal** in hello Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="44319-108">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Publicatieportal][api-management-management-console]

> <span data-ttu-id="44319-110">Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="44319-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="44319-111">Selecteer Hallo gewenste API in de publicatieportal hello en selecteer vervolgens Hallo **Operations** tabblad.</span><span class="sxs-lookup"><span data-stu-id="44319-111">Select hello desired API in hello publisher portal and then select hello **Operations** tab.</span></span> 

![Bewerkingen][api-management-operations]

<span data-ttu-id="44319-113">Klik op **bewerking toevoegen** tooadd een nieuwe bewerking.</span><span class="sxs-lookup"><span data-stu-id="44319-113">Click **Add Operation** tooadd a new operation.</span></span> <span data-ttu-id="44319-114">Hallo **nieuwe bewerking** wordt weergegeven en Hallo **handtekening** tabblad wordt standaard geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="44319-114">hello **New operation** will be displayed and hello **Signature** tab will be selected by default.</span></span>

![Bewerking toevoegen][api-management-add-operation]

<span data-ttu-id="44319-116">Geef Hallo **HTTP-term** door in de vervolgkeuzelijst hello te kiezen.</span><span class="sxs-lookup"><span data-stu-id="44319-116">Specify hello **HTTP verb** by choosing from hello drop-down list.</span></span>

![HTTP-methode][api-management-http-method]

<a name="url-template"></a>

<span data-ttu-id="44319-118">Hallo URL sjabloon door te typen in een URL-fragment die bestaan uit een of meer URL-padsegmenten en nul of meer queryreeksparameters definiëren.</span><span class="sxs-lookup"><span data-stu-id="44319-118">Define hello URL template by typing in a URL fragment consisting of one or more URL path segments and zero or more query string parameters.</span></span> <span data-ttu-id="44319-119">Hallo URL sjabloon, toegevoegde toohello basis-URL van Hallo API, identificeert één HTTP-bewerking.</span><span class="sxs-lookup"><span data-stu-id="44319-119">hello URL template, appended toohello base URL of hello API, identifies a single HTTP operation.</span></span> <span data-ttu-id="44319-120">Bevat een of meer benoemde variabele onderdelen die zijn geïdentificeerd door accolades.</span><span class="sxs-lookup"><span data-stu-id="44319-120">It may contain one or more named variable parts that are identified by curly braces.</span></span> <span data-ttu-id="44319-121">Deze variabele delen Sjabloonparameters worden genoemd en worden de waarden die worden opgehaald uit het Hallo-aanvraag-URL wanneer het Hallo-aanvraag wordt verwerkt door Hallo API Management-platform dynamisch toegewezen.</span><span class="sxs-lookup"><span data-stu-id="44319-121">These variable parts are called template parameters and are dynamically assigned values extracted from hello request's URL when hello request is being processed by hello API Management platform.</span></span>

> <span data-ttu-id="44319-122">Hallo URL sjabloon kan jokertekenpatronen bevatten.</span><span class="sxs-lookup"><span data-stu-id="44319-122">hello URL template can include wildcard patterns.</span></span> <span data-ttu-id="44319-123">Bijvoorbeeld, geven `/*` sturen alle aanvragen voor deze HTTP-methode toohello terug eindigt service.</span><span class="sxs-lookup"><span data-stu-id="44319-123">For example, specifying `/*` will forward all requests for that HTTP method toohello back end service.</span></span>

![URL-sjabloon][api-management-url-template]

<a name="rewrite-url-template"></a>

<span data-ttu-id="44319-125">Geef desgewenst Hallo **herschrijven van URL sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="44319-125">If desired, specify hello **Rewrite URL template**.</span></span> <span data-ttu-id="44319-126">Hiermee kunt u toouse Hallo standaard URL-sjabloon voor het verwerken van inkomende aanvragen op de front-hello, tijdens het aanroepen van Hallo back-end via een geconverteerde URL volgens toohello Herschrijf de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="44319-126">This allows you toouse hello standard URL template for processing incoming requests on hello front-end, while calling hello back-end via a converted URL according toohello rewrite template.</span></span> <span data-ttu-id="44319-127">Sjabloonparameters van Hallo URL sjabloon moeten worden gebruikt in Hallo herschrijven sjabloon.</span><span class="sxs-lookup"><span data-stu-id="44319-127">Template parameters from hello URL template should be used in hello rewrite template.</span></span> <span data-ttu-id="44319-128">Hallo volgende voorbeeld ziet u hoe inhoudstype gecodeerd zoals padsegment in de webservice Hallo uit het vorige voorbeeld Hallo kan worden opgegeven als een queryparameter in Hallo dat API gepubliceerd via Hallo Hallo URL sjablonen met behulp van API Management-platform.</span><span class="sxs-lookup"><span data-stu-id="44319-128">hello following example shows how content type encoded as path segment in hello web service from hello previous example can be provided as a query parameter in hello API published via hello API Management platform using hello URL templates.</span></span>

![Herschrijven van URL-sjabloon][api-management-url-template-rewrite]

<span data-ttu-id="44319-130">Gebruikmaken van aanroepfuncties toohello bewerking Hallo indeling `/customers?customerid=ALFKI` en dit te worden toegewezen`/Customers('ALFKI')` wanneer Hallo back-end-service wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="44319-130">Callers toohello operation will use hello format `/customers?customerid=ALFKI` and this will be mapped too`/Customers('ALFKI')` when hello back-end service is invoked.</span></span>

<span data-ttu-id="44319-131">**Weergave** naam en **beschrijving** Geef een beschrijving van de bewerking Hallo en gebruikte tooprovide documentatie zijn toohello ontwikkelaars met behulp van deze API in Hallo developer portal.</span><span class="sxs-lookup"><span data-stu-id="44319-131">**Display** name and **Description** provide a description of hello operation and are used tooprovide documentation toohello developers using this API in hello developer portal.</span></span>

![Beschrijving][api-management-description]

<span data-ttu-id="44319-133">Hallo bewerking beschrijving kan worden opgegeven als tekst zonder opmaak of HTML in Hallo **beschrijving** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="44319-133">hello operation description can be specified as plain text or HTML in hello **Description** text box.</span></span>

## <span data-ttu-id="44319-134"><a name="operation-caching"></a>Bewerking opslaan in cache</span><span class="sxs-lookup"><span data-stu-id="44319-134"><a name="operation-caching"> </a>Operation caching</span></span>
<span data-ttu-id="44319-135">Antwoord in cache opslaan vermindert de latentie waargenomen door de consument Hallo API, verlaagt bandbreedteverbruik en afname Hallo belasting op het Hallo HTTP web service implementeren Hallo API.</span><span class="sxs-lookup"><span data-stu-id="44319-135">Response caching reduces latency perceived by hello API consumers, lowers bandwidth consumption and decreases hello load on hello HTTP web service implementing hello API.</span></span> 

<span data-ttu-id="44319-136">tooeasily en snel geschikt maken voor Hallo bewerking, selecteer Hallo caching **opslaan in cache** tabblad en controleer Hallo **inschakelen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="44319-136">tooeasily and quickly enable caching for hello operation, select hello **Caching** tab and check hello **Enable** checkbox.</span></span>

![Caching][api-management-caching-tab]

<span data-ttu-id="44319-138">**Duur** Hallo periode gedurende welke Hallo bewerkingsantwoord in cache Hallo blijft bevat.</span><span class="sxs-lookup"><span data-stu-id="44319-138">**Duration** specifies hello time period during which hello operation response remains in hello cache.</span></span> <span data-ttu-id="44319-139">Hallo-standaardwaarde is 3600 seconden oftewel 1 uur.</span><span class="sxs-lookup"><span data-stu-id="44319-139">hello default value is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="44319-140">Cache-sleutels zijn gebruikte toodifferentiate tussen antwoorden zodat Hallo-antwoord overeenkomt tooeach verschillende Cachesleutel een eigen afzonderlijke waarde in de cache krijgt.</span><span class="sxs-lookup"><span data-stu-id="44319-140">Cache keys are used toodifferentiate between responses so that hello response corresponding tooeach different cache key will get its own separate cached value.</span></span> <span data-ttu-id="44319-141">Voer desgewenst specifieke queryreeksparameters en/of HTTP-headers toobe gebruikt in de cache-sleutelwaarden in Hallo computing **variëren op queryreeksparameters** en **variëren op headers** tekstvakken respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="44319-141">Optionally, enter specific query string parameters and/or HTTP headers toobe used in computing cache key values in hello **Vary by query string parameters** and **Vary by headers** text boxes respectively.</span></span> <span data-ttu-id="44319-142">Wanneer er geen is opgegeven, volledige aanvraag-URL en Hallo volgende HTTP-headerwaarden worden gebruikt in de cache genereren van sleutels: **accepteren** en **Accept-Charset**.</span><span class="sxs-lookup"><span data-stu-id="44319-142">When none are specified, full request URL and hello following HTTP header values are used in cache key generation: **Accept** and **Accept-Charset**.</span></span>

> <span data-ttu-id="44319-143">Zie voor meer informatie over opslaan in cache en cachebeleidsregels [hoe toocache bewerking resulteert in Azure API Management][How toocache operation results in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="44319-143">For more information on caching and caching policies, see [How toocache operation results in Azure API Management][How toocache operation results in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="44319-144"><a name="request-parameters"></a>Aanvraagparameters</span><span class="sxs-lookup"><span data-stu-id="44319-144"><a name="request-parameters"> </a>Request parameters</span></span>
<span data-ttu-id="44319-145">Bewerkingsparameters worden beheerd op het tabblad Hallo-Parameters. Parameters die zijn opgegeven in Hallo **URL sjabloon** op Hallo **handtekening** tabblad worden automatisch toegevoegd en kan worden gewijzigd alleen Hallo URL door sjabloon te bewerken.</span><span class="sxs-lookup"><span data-stu-id="44319-145">Operation parameters are managed on hello Parameters tab. Parameters specified in hello **URL Template** on hello **Signature** tab are added automatically and can be changed only by editing hello URL template.</span></span> <span data-ttu-id="44319-146">Extra parameters kunnen handmatig worden ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="44319-146">Additional parameters can be entered manually.</span></span>

<span data-ttu-id="44319-147">een nieuwe queryparameter tooadd klikt u op **queryparameter toevoegen** en voer de volgende informatie Hallo:</span><span class="sxs-lookup"><span data-stu-id="44319-147">tooadd a new query parameter, click **Add Query Parameter** and enter hello following information:</span></span>

* <span data-ttu-id="44319-148">**Naam** -parameternaam.</span><span class="sxs-lookup"><span data-stu-id="44319-148">**Name** - parameter name.</span></span>
* <span data-ttu-id="44319-149">**Beschrijving** -een korte beschrijving van het Hallo-parameter (optioneel).</span><span class="sxs-lookup"><span data-stu-id="44319-149">**Description** - a brief description of hello parameter (optional).</span></span>
* <span data-ttu-id="44319-150">**Type** -type voor parameter in de vervolgkeuzelijst Hallo geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="44319-150">**Type** - parameter type, selected in hello drop down.</span></span>
* <span data-ttu-id="44319-151">**Waarden** -waarden die kunnen worden toegewezen toothis-parameter.</span><span class="sxs-lookup"><span data-stu-id="44319-151">**Values** - values that can be assigned toothis parameter.</span></span> <span data-ttu-id="44319-152">Hallo-waarden kan worden als standaardwaarde gemarkeerd (optioneel).</span><span class="sxs-lookup"><span data-stu-id="44319-152">One of hello values can be marked as default (optional).</span></span>
* <span data-ttu-id="44319-153">**Vereist** -Hallo parameter verplicht te stellen door Hallo selectievakje.</span><span class="sxs-lookup"><span data-stu-id="44319-153">**Required** - make hello parameter mandatory by checking hello checkbox.</span></span> 

![Parameters van de aanvraag][api-management-request-parameters]

## <span data-ttu-id="44319-155"><a name="request-body"></a>Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="44319-155"><a name="request-body"> </a>Request body</span></span>
<span data-ttu-id="44319-156">Als het Hallo-bewerking staat (bijvoorbeeld PUT, POST) en kunt u desgewenst een voorbeeld van dit voor alle Hallo hoofdtekst ondersteunde weergave-indelingen (bijvoorbeeld json, XML) vereist.</span><span class="sxs-lookup"><span data-stu-id="44319-156">If hello operation allows (e.g. PUT, POST) and requires a body you may provide an example of it in all of hello supported representation formats (e.g. json, XML).</span></span> 

> <span data-ttu-id="44319-157">Hallo aanvraagtekst alleen voor documentatie wordt gebruikt en niet wordt gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="44319-157">hello request body is used for documentation purposes only and is not validated.</span></span>
> 
> 

<span data-ttu-id="44319-158">een aanvraagtekst tooenter overschakelen toohello **hoofdtekst** tabblad.</span><span class="sxs-lookup"><span data-stu-id="44319-158">tooenter a request body, switch toohello **Body** tab.</span></span>

<span data-ttu-id="44319-159">Klik op **weergave toevoegen**begint te typen gewenste inhoudstype-naam (bijvoorbeeld application/json), selecteert u deze in de vervolgkeuzelijst Hallo en plakken Hallo voorbeeld van de aanvraag hoofdtekst in geselecteerde Hallo-indeling in het tekstvak Hallo gewenst.</span><span class="sxs-lookup"><span data-stu-id="44319-159">Click **Add Representation**, start typing desired content type name (e.g. application/json), select it in hello drop-down, and paste hello desired request body example in hello selected format into hello text box.</span></span> 

![Aanvraagtekst][api-management-request-body]

<span data-ttu-id="44319-161">In de aanvullende toorepresentations, kunt u ook een optionele beschrijving in Hallo opgeven **beschrijving** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="44319-161">In additional toorepresentations, you can also specify an optional text description in hello **Description** text box.</span></span>

## <span data-ttu-id="44319-162"><a name="responses"></a>Antwoorden</span><span class="sxs-lookup"><span data-stu-id="44319-162"><a name="responses"> </a>Responses</span></span>
<span data-ttu-id="44319-163">Het is een goede gewoonte tooprovide voorbeelden van reacties voor alle statuscodes die Hallo-bewerking kan opleveren.</span><span class="sxs-lookup"><span data-stu-id="44319-163">It is a good practice tooprovide examples of responses for all status codes that hello operation may produce.</span></span> <span data-ttu-id="44319-164">Elke statuscode mogelijk meer dan één antwoord hoofdtekst voorbeeld, één voor elk Hallo inhoudstypen ondersteund.</span><span class="sxs-lookup"><span data-stu-id="44319-164">Each status code may have more than one response body example, one for each of hello supported content types.</span></span> 

<span data-ttu-id="44319-165">een antwoord tooadd klikt u op **toevoegen** en typ de gewenste Hallo-statuscode.</span><span class="sxs-lookup"><span data-stu-id="44319-165">tooadd a response, click **Add** and start typing hello desired status code.</span></span> <span data-ttu-id="44319-166">In dit voorbeeld Hallo status code is **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="44319-166">In this example hello status code is **200 OK**.</span></span> <span data-ttu-id="44319-167">Zodra het Hallo-code wordt weergegeven in de vervolgkeuzelijst hello, selecteren en Hallo antwoordcode is gemaakt en toegevoegd tooyour bewerking.</span><span class="sxs-lookup"><span data-stu-id="44319-167">Once hello code is displayed in hello drop-down, select it, and hello response code is created and added tooyour operation.</span></span>

![Reactiecode][api-management-response-code]

<span data-ttu-id="44319-169">Klik op **weergave toevoegen**, typ de naam van de gewenste inhoudstype hello (bijvoorbeeld application/json) en selecteer vervolgens in Hallo vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="44319-169">Click **Add Representation**, start typing hello desired content type name (e.g. application/json) and then select it in hello drop down.</span></span>

![Inhoudstype voor hoofdtekst][api-management-response-body-content-type]

<span data-ttu-id="44319-171">Hallo antwoord hoofdtekst voorbeeld in de geselecteerde indeling Hallo in Hallo tekstvak plakken.</span><span class="sxs-lookup"><span data-stu-id="44319-171">Paste hello response body example in hello selected format into hello text box.</span></span> 

![Antwoordtekst][api-management-response-body]

<span data-ttu-id="44319-173">Indien gewenst, voer een optionele beschrijving in Hallo **beschrijving** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="44319-173">If desired, add an optional description into hello **Description** text box.</span></span>

<span data-ttu-id="44319-174">Zodra het Hallo-bewerking is geconfigureerd, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="44319-174">Once hello operation is configured, click **Save**.</span></span>

## <span data-ttu-id="44319-175"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="44319-175"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="44319-176">Nadat Hallo bewerkingen zijn tooan API toegevoegd, wordt de volgende stap Hallo tooassociate Hallo API met een product is en deze publiceren zodat ontwikkelaars kunnen aanroepen op de operations.</span><span class="sxs-lookup"><span data-stu-id="44319-176">Once hello operations are added tooan API, hello next step is tooassociate hello API with a product and publish it so that developers can call its operations.</span></span>

* <span data-ttu-id="44319-177">[Hoe toocreate en een product publiceren][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="44319-177">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
