---
title: aaaAdd opslaan in cache tooimprove prestaties in Azure API Management | Microsoft Docs
description: Meer informatie over hoe tooimprove Hallo latentie, bandbreedtegebruik en webservice voor API Management-serviceaanroepen geladen.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a><span data-ttu-id="51d3d-103">Toevoegen van cachebewerkingen tooimprove prestaties in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="51d3d-103">Add caching tooimprove performance in Azure API Management</span></span>
<span data-ttu-id="51d3d-104">Bewerkingen in API Management kunnen worden geconfigureerd voor het opslaan van antwoorden in de cache.</span><span class="sxs-lookup"><span data-stu-id="51d3d-104">Operations in API Management can be configured for response caching.</span></span> <span data-ttu-id="51d3d-105">Door het opslaan van antwoorden in de cache kan de API-latentie, het bandbreedteverbruik en de webservicewerklast aanzienlijk worden verminderd voor gegevens die niet vaak wijzigen.</span><span class="sxs-lookup"><span data-stu-id="51d3d-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span></span>

<span data-ttu-id="51d3d-106">Deze handleiding ontdekt u hoe tooadd antwoord in cache opslaan voor uw API en beleidsregels voor Hallo voorbeeld-Echo-API-bewerkingen te configureren.</span><span class="sxs-lookup"><span data-stu-id="51d3d-106">This guide shows you how tooadd response caching for your API and configure policies for hello sample Echo API operations.</span></span> <span data-ttu-id="51d3d-107">U kunt vervolgens Hallo bewerking aanroepen vanuit het Hallo developer portal tooverify cache in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="51d3d-107">You can then call hello operation from hello developer portal tooverify caching in action.</span></span>

> [!NOTE]
> <span data-ttu-id="51d3d-108">Zie [Aangepast opslaan in cache in Azure API Management](api-management-sample-cache-by-key.md) voor informatie over het opslaan van items in de cache per sleutel met behulp van beleidsexpressies.</span><span class="sxs-lookup"><span data-stu-id="51d3d-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="51d3d-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="51d3d-109">Prerequisites</span></span>
<span data-ttu-id="51d3d-110">Voordat de volgende Hallo stappen in deze handleiding, hebt u een API Management-service-exemplaar met een API en een product dat is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="51d3d-110">Before following hello steps in this guide, you must have an API Management service instance with an API and a product configured.</span></span> <span data-ttu-id="51d3d-111">Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="51d3d-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

## <span data-ttu-id="51d3d-112"><a name="configure-caching"> </a>Een bewerking voor opslaan in cache configureren</span><span class="sxs-lookup"><span data-stu-id="51d3d-112"><a name="configure-caching"> </a>Configure an operation for caching</span></span>
<span data-ttu-id="51d3d-113">In deze stap controleert u opslaan in cache-instellingen van Hallo Hallo **GET Resource (in cache)** bewerking van Hallo voorbeeld-Echo-API.</span><span class="sxs-lookup"><span data-stu-id="51d3d-113">In this step, you will review hello caching settings of hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

> [!NOTE]
> <span data-ttu-id="51d3d-114">Elk exemplaar van API Management-service is vooraf geconfigureerd met een Echo-API die kan worden gebruikt tooexperiment met en meer informatie over API Management.</span><span class="sxs-lookup"><span data-stu-id="51d3d-114">Each API Management service instance comes preconfigured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="51d3d-115">Zie [Aan de slag met Azure API Management][Get started with Azure API Management] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="51d3d-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span></span>
> 
> 

<span data-ttu-id="51d3d-116">tooget gestart, klikt u op **publicatieportal** in hello Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="51d3d-116">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="51d3d-117">Hiermee gaat u toohello API Management-publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="51d3d-117">This takes you toohello API Management publisher portal.</span></span>

![Publicatieportal][api-management-management-console]

<span data-ttu-id="51d3d-119">Klik op **API's** van Hallo **API Management** menu op Hallo links en klik vervolgens op **Echo-API**.</span><span class="sxs-lookup"><span data-stu-id="51d3d-119">Click **APIs** from hello **API Management** menu on hello left, and then click **Echo API**.</span></span>

![Echo-API][api-management-echo-api]

<span data-ttu-id="51d3d-121">Klik op Hallo **Operations** tabblad en klik vervolgens op Hallo **GET Resource (in cache)** bewerking Hallo **Operations** lijst.</span><span class="sxs-lookup"><span data-stu-id="51d3d-121">Click hello **Operations** tab, and then click hello **GET Resource (cached)** operation from hello **Operations** list.</span></span>

![Bewerkingen Echo-API][api-management-echo-api-operations]

<span data-ttu-id="51d3d-123">Klik op Hallo **opslaan in cache** tabblad tooview Hallo opslaan in cache-instellingen voor deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="51d3d-123">Click hello **Caching** tab tooview hello caching settings for this operation.</span></span>

![Tabblad Opslaan in cache][api-management-caching-tab]

<span data-ttu-id="51d3d-125">tooenable cache voor een bewerking, selecteer Hallo **inschakelen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="51d3d-125">tooenable caching for an operation, select hello **Enable** check box.</span></span> <span data-ttu-id="51d3d-126">In dit voorbeeld is opslaan in cache ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="51d3d-126">In this example, caching is enabled.</span></span>

<span data-ttu-id="51d3d-127">Het bewerkingsantwoord van elke sleutelhash op basis van waarden in Hallo Hallo **variëren op queryreeksparameters** en **variëren op headers** velden.</span><span class="sxs-lookup"><span data-stu-id="51d3d-127">Each operation response is keyed, based on hello values in hello **Vary by query string parameters** and **Vary by headers** fields.</span></span> <span data-ttu-id="51d3d-128">Als u meerdere antwoorden op basis van queryreeksparameters of headers toocache wilt, kunt u ze configureren in deze twee velden.</span><span class="sxs-lookup"><span data-stu-id="51d3d-128">If you want toocache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span></span>

<span data-ttu-id="51d3d-129">**Duur** wordt Hallo Vervalinterval opgegeven van Hallo in de cache opgeslagen reacties.</span><span class="sxs-lookup"><span data-stu-id="51d3d-129">**Duration** specifies hello expiration interval of hello cached responses.</span></span> <span data-ttu-id="51d3d-130">In dit voorbeeld hello-interval is **3600** seconden, dat gelijkwaardige tooone uur.</span><span class="sxs-lookup"><span data-stu-id="51d3d-130">In this example, hello interval is **3600** seconds, which is equivalent tooone hour.</span></span>

<span data-ttu-id="51d3d-131">Eerste aanvraag toohello Hallo opslaan in cache configureren in dit voorbeeld gebruikt, Hallo **GET Resource (in cache)** bewerking een antwoord geretourneerd van Hallo back-endservice.</span><span class="sxs-lookup"><span data-stu-id="51d3d-131">Using hello caching configuration in this example, hello first request toohello **GET Resource (cached)** operation returns a response from hello backend service.</span></span> <span data-ttu-id="51d3d-132">Dit antwoord wordt in de cache opgeslagen, ingevoerd met Hallo opgegeven headers en query tekenreeksparameters.</span><span class="sxs-lookup"><span data-stu-id="51d3d-132">This response will be cached, keyed by hello specified headers and query string parameters.</span></span> <span data-ttu-id="51d3d-133">Volgende aanroepen toohello bewerking, met overeenkomende parameters, Hallo hebben in de cache opgeslagen antwoord geretourneerd totdat Hallo cacheduurinterval is verlopen.</span><span class="sxs-lookup"><span data-stu-id="51d3d-133">Subsequent calls toohello operation, with matching parameters, will have hello cached response returned, until hello cache duration interval has expired.</span></span>

## <span data-ttu-id="51d3d-134"><a name="caching-policies"></a>Revisie Hallo cachebeleidsregels</span><span class="sxs-lookup"><span data-stu-id="51d3d-134"><a name="caching-policies"> </a>Review hello caching policies</span></span>
<span data-ttu-id="51d3d-135">In deze stap controleert u opslaan in cache-instellingen voor Hallo Hallo **GET Resource (in cache)** bewerking van Hallo voorbeeld-Echo-API.</span><span class="sxs-lookup"><span data-stu-id="51d3d-135">In this step, you review hello caching settings for hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

<span data-ttu-id="51d3d-136">Wanneer er cache-instellingen zijn geconfigureerd voor een bewerking op Hallo **opslaan in cache** tabblad opslaan in cache toegevoegd voor Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="51d3d-136">When caching settings are configured for an operation on hello **Caching** tab, caching policies are added for hello operation.</span></span> <span data-ttu-id="51d3d-137">Deze beleidsregels kunnen worden bekeken en bewerkt in de beleidseditor Hallo.</span><span class="sxs-lookup"><span data-stu-id="51d3d-137">These policies can be viewed and edited in hello policy editor.</span></span>

<span data-ttu-id="51d3d-138">Klik op **beleid** van Hallo **API Management** menu op Hallo linker- en selecteer vervolgens **Echo-API / GET Resource (in cache)** van Hallo **bewerking**vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="51d3d-138">Click **Policies** from hello **API Management** menu on hello left, and then select **Echo API / GET Resource (cached)** from hello **Operation** drop-down list.</span></span>

![Bewerking beleidsbereik][api-management-operation-dropdown]

<span data-ttu-id="51d3d-140">Hallo-beleid voor deze bewerking weergegeven in de beleidseditor Hallo.</span><span class="sxs-lookup"><span data-stu-id="51d3d-140">This displays hello policies for this operation in hello policy editor.</span></span>

![Beleidseditor API Management][api-management-policy-editor]

<span data-ttu-id="51d3d-142">Hallo beleidsdefinitie voor deze bewerking bevat Hallo beleidsregels waarmee Hallo caching configuratie gedefinieerd, die is gecontroleerd met Hallo **opslaan in cache** tabblad in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="51d3d-142">hello policy definition for this operation includes hello policies that define hello caching configuration that were reviewed using hello **Caching** tab in hello previous step.</span></span>

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> <span data-ttu-id="51d3d-143">Wijzigingen toohello cachebeleidsregels in de beleidseditor hello, worden weergegeven op Hallo **opslaan in cache** tabblad van een bewerking en vice versa.</span><span class="sxs-lookup"><span data-stu-id="51d3d-143">Changes made toohello caching policies in hello policy editor will be reflected on hello **Caching** tab of an operation, and vice-versa.</span></span>
> 
> 

## <span data-ttu-id="51d3d-144"><a name="test-operation"></a>Een bewerking aanroepen en Hallo opslaan in cache testen</span><span class="sxs-lookup"><span data-stu-id="51d3d-144"><a name="test-operation"> </a>Call an operation and test hello caching</span></span>
<span data-ttu-id="51d3d-145">toosee hello caching in actie, kunnen we Hallo bewerking aanroepen vanuit Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="51d3d-145">toosee hello caching in action, we can call hello operation from hello developer portal.</span></span> <span data-ttu-id="51d3d-146">Klik op **ontwikkelaarsportal** in Hallo menu rechtsboven.</span><span class="sxs-lookup"><span data-stu-id="51d3d-146">Click **Developer portal** in hello top right menu.</span></span>

![ontwikkelaarsportal][api-management-developer-portal-menu]

<span data-ttu-id="51d3d-148">Klik op **API's** in Hallo bovenste menu en selecteer vervolgens **Echo-API**.</span><span class="sxs-lookup"><span data-stu-id="51d3d-148">Click **APIs** in hello top menu, and then select **Echo API**.</span></span>

![Echo-API][api-management-apis-echo-api]

> <span data-ttu-id="51d3d-150">Als er slechts één API is geconfigureerd of zichtbaar tooyour-account op de API's te klikken u rechtstreeks toohello bewerkingen voor die API gaat.</span><span class="sxs-lookup"><span data-stu-id="51d3d-150">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="51d3d-151">Selecteer Hallo **GET Resource (in cache)** bewerking en klik vervolgens op **Console openen**.</span><span class="sxs-lookup"><span data-stu-id="51d3d-151">Select hello **GET Resource (cached)** operation, and then click **Open Console**.</span></span>

![Console openen][api-management-open-console]

<span data-ttu-id="51d3d-153">Hallo-console kunt u bewerkingen rechtstreeks vanuit de ontwikkelaarsportal hello tooinvoke.</span><span class="sxs-lookup"><span data-stu-id="51d3d-153">hello console allows you tooinvoke operations directly from hello developer portal.</span></span>

![Console][api-management-console]

<span data-ttu-id="51d3d-155">Behoud de standaardwaarden Hallo voor **param1** en **param2**.</span><span class="sxs-lookup"><span data-stu-id="51d3d-155">Keep hello default values for **param1** and **param2**.</span></span>

<span data-ttu-id="51d3d-156">Selecteer de gewenste sleutel in Hallo Hallo **abonnementssleutel** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="51d3d-156">Select hello desired key from hello **subscription-key** drop-down list.</span></span> <span data-ttu-id="51d3d-157">Als uw account slechts één abonnement heeft, is de sleutel al geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="51d3d-157">If your account has only one subscription, it will already be selected.</span></span>

<span data-ttu-id="51d3d-158">Voer **sampleheader: Value1** in Hallo **aanvraagheaders** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="51d3d-158">Enter **sampleheader:value1** in hello **Request headers** text box.</span></span>

<span data-ttu-id="51d3d-159">Klik op **HTTP Get** en maak een notitie van Hallo antwoordheaders.</span><span class="sxs-lookup"><span data-stu-id="51d3d-159">Click **HTTP Get** and make a note of hello response headers.</span></span>

<span data-ttu-id="51d3d-160">Voer **sampleheader: Value2** in Hallo **aanvraagheaders** in het tekstvak en klik vervolgens op **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="51d3d-160">Enter **sampleheader:value2** in hello **Request headers** text box, and then click **HTTP Get**.</span></span>

<span data-ttu-id="51d3d-161">Houd er rekening mee dat Hallo de waarde van **sampleheader** nog steeds **value1** Hallo reactie.</span><span class="sxs-lookup"><span data-stu-id="51d3d-161">Note that hello value of **sampleheader** is still **value1** in hello response.</span></span> <span data-ttu-id="51d3d-162">Probeer een aantal verschillende waarden en merk op dat in de cache opgeslagen reactie van de eerste aanroep Hallo Hallo wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="51d3d-162">Try some different values and note that hello cached response from hello first call is returned.</span></span>

<span data-ttu-id="51d3d-163">Voer **25** in Hallo **param2** veld en klik vervolgens op **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="51d3d-163">Enter **25** into hello **param2** field, and then click **HTTP Get**.</span></span>

<span data-ttu-id="51d3d-164">Houd er rekening mee dat Hallo de waarde van **sampleheader** in Hallo antwoord is nu **value2**.</span><span class="sxs-lookup"><span data-stu-id="51d3d-164">Note that hello value of **sampleheader** in hello response is now **value2**.</span></span> <span data-ttu-id="51d3d-165">Omdat Hallo per querytekenreeks Bewerkingsresultaten, Hallo vorige cacheantwoord niet geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="51d3d-165">Because hello operation results are keyed by query string, hello previous cached response was not returned.</span></span>

## <span data-ttu-id="51d3d-166"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="51d3d-166"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="51d3d-167">Zie voor meer informatie over cachebeleidsregels [cachebeleidsregels] [ Caching policies] in Hallo [documentatie voor API Management-beleid][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="51d3d-167">For more information about caching policies, see [Caching policies][Caching policies] in hello [API Management policy reference][API Management policy reference].</span></span>
* <span data-ttu-id="51d3d-168">Zie [Aangepast opslaan in cache in Azure API Management](api-management-sample-cache-by-key.md) voor informatie over het opslaan van items in de cache per sleutel met behulp van beleidsexpressies.</span><span class="sxs-lookup"><span data-stu-id="51d3d-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
