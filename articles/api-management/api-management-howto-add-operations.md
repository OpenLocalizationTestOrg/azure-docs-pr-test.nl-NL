---
title: Bewerkingen toevoegen aan een API in Azure API Management | Microsoft Docs
description: Informatie over het bewerkingen toevoegen aan een API in Azure API Management.
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
ms.openlocfilehash: 105fc51c2d1152a40a5757985da47330e0b7b8cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-operations-to-an-api-in-azure-api-management"></a><span data-ttu-id="2e865-103">Bewerkingen toevoegen aan een API in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="2e865-103">How to add operations to an API in Azure API Management</span></span>
<span data-ttu-id="2e865-104">Voordat een API in API Management kan worden gebruikt, kunnen bewerkingen moeten worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="2e865-104">Before an API in API Management can be used, operations must be added.</span></span> <span data-ttu-id="2e865-105">Deze handleiding laat zien hoe toevoegen en configureren van verschillende typen aan een API-bewerkingen in API Management.</span><span class="sxs-lookup"><span data-stu-id="2e865-105">This guide shows how to add and configure different types of operations to an API in API Management.</span></span>

## <span data-ttu-id="2e865-106"><a name="add-operation"></a>Een bewerking toevoegen</span><span class="sxs-lookup"><span data-stu-id="2e865-106"><a name="add-operation"> </a>Add an operation</span></span>
<span data-ttu-id="2e865-107">Bewerkingen zijn toegevoegd en geconfigureerd voor een API in de publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="2e865-107">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="2e865-108">Voor toegang tot de publicatieportal bevindt, klikt u op **publicatieportal** in de Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="2e865-108">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Publicatieportal][api-management-management-console]

> <span data-ttu-id="2e865-110">Als u nog geen service-exemplaar van API Management hebt gemaakt, raadpleegt u [Service-exemplaar van API Management maken][Create an API Management service instance] in de zelfstudie [Aan de slag met Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="2e865-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="2e865-111">Selecteer de gewenste API in de publicatieportal en selecteer vervolgens de **Operations** tabblad.</span><span class="sxs-lookup"><span data-stu-id="2e865-111">Select the desired API in the publisher portal and then select the **Operations** tab.</span></span> 

![Bewerkingen][api-management-operations]

<span data-ttu-id="2e865-113">Klik op **bewerking toevoegen** toevoegen van een nieuwe bewerking.</span><span class="sxs-lookup"><span data-stu-id="2e865-113">Click **Add Operation** to add a new operation.</span></span> <span data-ttu-id="2e865-114">De **nieuwe bewerking** wordt weergegeven en de **handtekening** tabblad wordt standaard geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="2e865-114">The **New operation** will be displayed and the **Signature** tab will be selected by default.</span></span>

![Bewerking toevoegen][api-management-add-operation]

<span data-ttu-id="2e865-116">Geef de **HTTP-term** door te kiezen uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="2e865-116">Specify the **HTTP verb** by choosing from the drop-down list.</span></span>

![HTTP-methode][api-management-http-method]

<a name="url-template"></a>

<span data-ttu-id="2e865-118">Definieer de URL-sjabloon door in een URL-fragment die bestaan uit een of meer URL-padsegmenten en nul of meer queryreeksparameters te typen.</span><span class="sxs-lookup"><span data-stu-id="2e865-118">Define the URL template by typing in a URL fragment consisting of one or more URL path segments and zero or more query string parameters.</span></span> <span data-ttu-id="2e865-119">De URL-sjabloon, toegevoegd aan de basis-URL van de API identificeert één HTTP-bewerking.</span><span class="sxs-lookup"><span data-stu-id="2e865-119">The URL template, appended to the base URL of the API, identifies a single HTTP operation.</span></span> <span data-ttu-id="2e865-120">Bevat een of meer benoemde variabele onderdelen die zijn geïdentificeerd door accolades.</span><span class="sxs-lookup"><span data-stu-id="2e865-120">It may contain one or more named variable parts that are identified by curly braces.</span></span> <span data-ttu-id="2e865-121">Deze variabele delen Sjabloonparameters worden genoemd en worden de waarden die worden opgehaald uit de aanvraag-URL wanneer de aanvraag wordt verwerkt door het platform van API Management dynamisch toegewezen.</span><span class="sxs-lookup"><span data-stu-id="2e865-121">These variable parts are called template parameters and are dynamically assigned values extracted from the request's URL when the request is being processed by the API Management platform.</span></span>

> <span data-ttu-id="2e865-122">De URL-sjabloon kan jokertekenpatronen bevatten.</span><span class="sxs-lookup"><span data-stu-id="2e865-122">The URL template can include wildcard patterns.</span></span> <span data-ttu-id="2e865-123">Bijvoorbeeld, geven `/*` wordt sturen alle aanvragen voor deze HTTP-methode voor de back-end service.</span><span class="sxs-lookup"><span data-stu-id="2e865-123">For example, specifying `/*` will forward all requests for that HTTP method to the back end service.</span></span>

![URL-sjabloon][api-management-url-template]

<a name="rewrite-url-template"></a>

<span data-ttu-id="2e865-125">Geef desgewenst de **herschrijven van URL sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="2e865-125">If desired, specify the **Rewrite URL template**.</span></span> <span data-ttu-id="2e865-126">Hiermee kunt u de standaard URL-sjabloon gebruiken voor het verwerken van inkomende aanvragen op de front-end tijdens het aanroepen van de back-end via een geconverteerde URL volgens de sjabloon opnieuw.</span><span class="sxs-lookup"><span data-stu-id="2e865-126">This allows you to use the standard URL template for processing incoming requests on the front-end, while calling the back-end via a converted URL according to the rewrite template.</span></span> <span data-ttu-id="2e865-127">Sjabloonparameters van de URL-sjabloon moeten worden gebruikt in de sjabloon opnieuw.</span><span class="sxs-lookup"><span data-stu-id="2e865-127">Template parameters from the URL template should be used in the rewrite template.</span></span> <span data-ttu-id="2e865-128">Het volgende voorbeeld ziet hoe inhoudstype gecodeerd zoals padsegment in de webservice van het vorige voorbeeld kan worden opgegeven als een queryparameter in de API gepubliceerd via het API Management-platform met behulp van de URL-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="2e865-128">The following example shows how content type encoded as path segment in the web service from the previous example can be provided as a query parameter in the API published via the API Management platform using the URL templates.</span></span>

![Herschrijven van URL-sjabloon][api-management-url-template-rewrite]

<span data-ttu-id="2e865-130">Aanroepfuncties voor de bewerking wordt de notatie gebruikt `/customers?customerid=ALFKI` en deze worden toegewezen aan `/Customers('ALFKI')` wanneer de back-endservice wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="2e865-130">Callers to the operation will use the format `/customers?customerid=ALFKI` and this will be mapped to `/Customers('ALFKI')` when the back-end service is invoked.</span></span>

<span data-ttu-id="2e865-131">**Weergave** naam en **beschrijving** Geef een beschrijving van de bewerking en worden gebruikt voor het bieden van documentatie voor de ontwikkelaars die met deze API in de portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="2e865-131">**Display** name and **Description** provide a description of the operation and are used to provide documentation to the developers using this API in the developer portal.</span></span>

![Beschrijving][api-management-description]

<span data-ttu-id="2e865-133">De beschrijving van de bewerking kan worden opgegeven als tekst zonder opmaak of HTML-code in de **beschrijving** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="2e865-133">The operation description can be specified as plain text or HTML in the **Description** text box.</span></span>

## <span data-ttu-id="2e865-134"><a name="operation-caching"></a>Bewerking opslaan in cache</span><span class="sxs-lookup"><span data-stu-id="2e865-134"><a name="operation-caching"> </a>Operation caching</span></span>
<span data-ttu-id="2e865-135">Antwoord in cache opslaan, vermindert de latentie waargenomen door de API-consumenten, verlaagt bandbreedteverbruik en vermindert de belasting van het HTTP-web service-implementatie van de API.</span><span class="sxs-lookup"><span data-stu-id="2e865-135">Response caching reduces latency perceived by the API consumers, lowers bandwidth consumption and decreases the load on the HTTP web service implementing the API.</span></span> 

<span data-ttu-id="2e865-136">Om snel en eenvoudig cachebewerkingen voor de bewerking, selecteer de **opslaan in cache** tabblad en controleer de **inschakelen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="2e865-136">To easily and quickly enable caching for the operation, select the **Caching** tab and check the **Enable** checkbox.</span></span>

![Caching][api-management-caching-tab]

<span data-ttu-id="2e865-138">**Duur** Hiermee geeft u de periode gedurende welke de bewerkingsantwoord in de cache blijft.</span><span class="sxs-lookup"><span data-stu-id="2e865-138">**Duration** specifies the time period during which the operation response remains in the cache.</span></span> <span data-ttu-id="2e865-139">De standaardwaarde is 3600 seconden oftewel 1 uur.</span><span class="sxs-lookup"><span data-stu-id="2e865-139">The default value is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="2e865-140">Cache-sleutels worden gebruikt om onderscheid maken tussen antwoorden zodat het overeenkomt met elk ander Cachesleutel antwoord een eigen afzonderlijke waarde in de cache krijgt.</span><span class="sxs-lookup"><span data-stu-id="2e865-140">Cache keys are used to differentiate between responses so that the response corresponding to each different cache key will get its own separate cached value.</span></span> <span data-ttu-id="2e865-141">U kunt desgewenst specifieke queryreeksparameters en/of HTTP-headers worden gebruikt in de cache sleutelwaarden in computing de **variëren op queryreeksparameters** en **variëren op headers** tekstvakken respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="2e865-141">Optionally, enter specific query string parameters and/or HTTP headers to be used in computing cache key values in the **Vary by query string parameters** and **Vary by headers** text boxes respectively.</span></span> <span data-ttu-id="2e865-142">Wanneer er geen is opgegeven, volledige aanvraag-URL en de volgende waarden van de HTTP-header worden gebruikt in de cache sleutelgeneratie: **accepteren** en **Accept-Charset**.</span><span class="sxs-lookup"><span data-stu-id="2e865-142">When none are specified, full request URL and the following HTTP header values are used in cache key generation: **Accept** and **Accept-Charset**.</span></span>

> <span data-ttu-id="2e865-143">Zie voor meer informatie over opslaan in cache en cachebeleidsregels [hoe in de cache van de bewerking resulteert in Azure API Management][How to cache operation results in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="2e865-143">For more information on caching and caching policies, see [How to cache operation results in Azure API Management][How to cache operation results in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="2e865-144"><a name="request-parameters"></a>Aanvraagparameters</span><span class="sxs-lookup"><span data-stu-id="2e865-144"><a name="request-parameters"> </a>Request parameters</span></span>
<span data-ttu-id="2e865-145">Bewerkingsparameters worden op het tabblad Parameters beheerd.</span><span class="sxs-lookup"><span data-stu-id="2e865-145">Operation parameters are managed on the Parameters tab.</span></span> <span data-ttu-id="2e865-146">Parameters die zijn opgegeven de **URL sjabloon** op de **handtekening** tabblad worden automatisch toegevoegd en kan alleen door het bewerken van het URL-sjabloon worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="2e865-146">Parameters specified in the **URL Template** on the **Signature** tab are added automatically and can be changed only by editing the URL template.</span></span> <span data-ttu-id="2e865-147">Extra parameters kunnen handmatig worden ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="2e865-147">Additional parameters can be entered manually.</span></span>

<span data-ttu-id="2e865-148">Klik op als u een nieuwe queryparameter **queryparameter toevoegen** en voer de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="2e865-148">To add a new query parameter, click **Add Query Parameter** and enter the following information:</span></span>

* <span data-ttu-id="2e865-149">**Naam** -parameternaam.</span><span class="sxs-lookup"><span data-stu-id="2e865-149">**Name** - parameter name.</span></span>
* <span data-ttu-id="2e865-150">**Beschrijving** -een korte beschrijving van de parameter (optioneel).</span><span class="sxs-lookup"><span data-stu-id="2e865-150">**Description** - a brief description of the parameter (optional).</span></span>
* <span data-ttu-id="2e865-151">**Type** -type voor parameter omlaag in de vervolgkeuzelijst is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="2e865-151">**Type** - parameter type, selected in the drop down.</span></span>
* <span data-ttu-id="2e865-152">**Waarden** -waarden die kunnen worden toegewezen aan deze parameter.</span><span class="sxs-lookup"><span data-stu-id="2e865-152">**Values** - values that can be assigned to this parameter.</span></span> <span data-ttu-id="2e865-153">Een van de waarden kan worden als standaardwaarde gemarkeerd (optioneel).</span><span class="sxs-lookup"><span data-stu-id="2e865-153">One of the values can be marked as default (optional).</span></span>
* <span data-ttu-id="2e865-154">**Vereist** -de parameter verplicht te stellen door het selectievakje.</span><span class="sxs-lookup"><span data-stu-id="2e865-154">**Required** - make the parameter mandatory by checking the checkbox.</span></span> 

![Parameters van de aanvraag][api-management-request-parameters]

## <span data-ttu-id="2e865-156"><a name="request-body"></a>Aanvraagtekst</span><span class="sxs-lookup"><span data-stu-id="2e865-156"><a name="request-body"> </a>Request body</span></span>
<span data-ttu-id="2e865-157">Als de bewerking kunt (bijvoorbeeld PUT, POST) en een hoofdtekst kunt u desgewenst een voorbeeld van dit voor alle van de ondersteunde weergave-indelingen (bijvoorbeeld json, XML) vereist.</span><span class="sxs-lookup"><span data-stu-id="2e865-157">If the operation allows (e.g. PUT, POST) and requires a body you may provide an example of it in all of the supported representation formats (e.g. json, XML).</span></span> 

> <span data-ttu-id="2e865-158">De aanvraagtekst alleen voor documentatie wordt gebruikt en niet wordt gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="2e865-158">The request body is used for documentation purposes only and is not validated.</span></span>
> 
> 

<span data-ttu-id="2e865-159">Als u wilt een aanvraagtekst invoeren, overschakelen naar de **hoofdtekst** tabblad.</span><span class="sxs-lookup"><span data-stu-id="2e865-159">To enter a request body, switch to the **Body** tab.</span></span>

<span data-ttu-id="2e865-160">Klik op **weergave toevoegen**, gewenste inhoudstype-naam (bijvoorbeeld application/json) begint te typen, selecteert u deze in de vervolgkeuzelijst en plak het gewenste aanvraag hoofdtekst voorbeeld in de geselecteerde indeling in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="2e865-160">Click **Add Representation**, start typing desired content type name (e.g. application/json), select it in the drop-down, and paste the desired request body example in the selected format into the text box.</span></span> 

![Aanvraagtekst][api-management-request-body]

<span data-ttu-id="2e865-162">Extra's worden representaties, u kunt ook opgeven in een optionele beschrijving in de **beschrijving** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="2e865-162">In additional to representations, you can also specify an optional text description in the **Description** text box.</span></span>

## <span data-ttu-id="2e865-163"><a name="responses"></a>Antwoorden</span><span class="sxs-lookup"><span data-stu-id="2e865-163"><a name="responses"> </a>Responses</span></span>
<span data-ttu-id="2e865-164">Het is raadzaam vindt u voorbeelden van reacties voor alle statuscodes die de bewerking kan opleveren.</span><span class="sxs-lookup"><span data-stu-id="2e865-164">It is a good practice to provide examples of responses for all status codes that the operation may produce.</span></span> <span data-ttu-id="2e865-165">Elke statuscode mogelijk meer dan één antwoord instantie bijvoorbeeld één voor elk van de ondersteunde typen inhoud.</span><span class="sxs-lookup"><span data-stu-id="2e865-165">Each status code may have more than one response body example, one for each of the supported content types.</span></span> 

<span data-ttu-id="2e865-166">Klik op als u een antwoord **toevoegen** en typ de gewenste statuscode.</span><span class="sxs-lookup"><span data-stu-id="2e865-166">To add a response, click **Add** and start typing the desired status code.</span></span> <span data-ttu-id="2e865-167">In dit voorbeeld de statuscode is **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="2e865-167">In this example the status code is **200 OK**.</span></span> <span data-ttu-id="2e865-168">Zodra de code wordt weergegeven in de vervolgkeuzelijst, selecteert u deze en de antwoordcode wordt gemaakt en toegevoegd aan de bewerking opnieuw.</span><span class="sxs-lookup"><span data-stu-id="2e865-168">Once the code is displayed in the drop-down, select it, and the response code is created and added to your operation.</span></span>

![Reactiecode][api-management-response-code]

<span data-ttu-id="2e865-170">Klik op **weergave toevoegen**, de naam van het gewenste type inhoud (bijvoorbeeld application/json) begint te typen en vervolgens omlaag in de vervolgkeuzelijst selecteren.</span><span class="sxs-lookup"><span data-stu-id="2e865-170">Click **Add Representation**, start typing the desired content type name (e.g. application/json) and then select it in the drop down.</span></span>

![Inhoudstype voor hoofdtekst][api-management-response-body-content-type]

<span data-ttu-id="2e865-172">Plak in het voorbeeld van de hoofdtekst van antwoord in de geselecteerde indeling in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="2e865-172">Paste the response body example in the selected format into the text box.</span></span> 

![Antwoordtekst][api-management-response-body]

<span data-ttu-id="2e865-174">Indien gewenst, voer een optionele beschrijving in de **beschrijving** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="2e865-174">If desired, add an optional description into the **Description** text box.</span></span>

<span data-ttu-id="2e865-175">Nadat de bewerking is geconfigureerd, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2e865-175">Once the operation is configured, click **Save**.</span></span>

## <span data-ttu-id="2e865-176"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2e865-176"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="2e865-177">Nadat de bewerkingen zijn toegevoegd aan een API, wordt de volgende stap is naar de API koppelen aan een product en deze publiceren zodat ontwikkelaars bewerkingen kunnen aanroepen.</span><span class="sxs-lookup"><span data-stu-id="2e865-177">Once the operations are added to an API, the next step is to associate the API with a product and publish it so that developers can call its operations.</span></span>

* <span data-ttu-id="2e865-178">[Het maken en een product publiceren][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="2e865-178">[How to create and publish a product][How to create and publish a product]</span></span>

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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to cache operation results in Azure API Management]: api-management-howto-cache.md
