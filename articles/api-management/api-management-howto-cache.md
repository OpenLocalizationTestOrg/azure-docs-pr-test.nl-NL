---
title: Opslaan in cache toevoegen om de prestaties in Azure API Management te verbeteren | Microsoft Docs
description: Informatie over het verbeteren van de latentie, het bandbreedteverbruik en de webservicewerklast voor API Management-serviceaanroepen.
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
ms.openlocfilehash: 59c595f0d5ce849f44c46fdb6cab0b44d35fffa0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-caching-to-improve-performance-in-azure-api-management"></a><span data-ttu-id="09acf-103">Opslaan in cache toevoegen om de prestaties in Azure API Management te verbeteren</span><span class="sxs-lookup"><span data-stu-id="09acf-103">Add caching to improve performance in Azure API Management</span></span>
<span data-ttu-id="09acf-104">Bewerkingen in API Management kunnen worden geconfigureerd voor het opslaan van antwoorden in de cache.</span><span class="sxs-lookup"><span data-stu-id="09acf-104">Operations in API Management can be configured for response caching.</span></span> <span data-ttu-id="09acf-105">Door het opslaan van antwoorden in de cache kan de API-latentie, het bandbreedteverbruik en de webservicewerklast aanzienlijk worden verminderd voor gegevens die niet vaak wijzigen.</span><span class="sxs-lookup"><span data-stu-id="09acf-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span></span>

<span data-ttu-id="09acf-106">In deze handleiding wordt getoond hoe u het opslaan van antwoorden in de cache toevoegt voor uw API en beleidsregels configureert voor de bewerkingen voor de voorbeeld-Echo-API.</span><span class="sxs-lookup"><span data-stu-id="09acf-106">This guide shows you how to add response caching for your API and configure policies for the sample Echo API operations.</span></span> <span data-ttu-id="09acf-107">U kunt de bewerking vervolgens aanroepen vanuit de ontwikkelaarsportal om te controleren of opslaan in de cache werkt.</span><span class="sxs-lookup"><span data-stu-id="09acf-107">You can then call the operation from the developer portal to verify caching in action.</span></span>

> [!NOTE]
> <span data-ttu-id="09acf-108">Zie [Aangepast opslaan in cache in Azure API Management](api-management-sample-cache-by-key.md) voor informatie over het opslaan van items in de cache per sleutel met behulp van beleidsexpressies.</span><span class="sxs-lookup"><span data-stu-id="09acf-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="09acf-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="09acf-109">Prerequisites</span></span>
<span data-ttu-id="09acf-110">Voordat u de stappen in deze handleiding volgt, moet u een service-exemplaar van API Management hebben waarvoor een API en een product zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="09acf-110">Before following the steps in this guide, you must have an API Management service instance with an API and a product configured.</span></span> <span data-ttu-id="09acf-111">Als u nog geen service-exemplaar van API Management hebt gemaakt, raadpleegt u [Service-exemplaar van API Management maken][Create an API Management service instance] in de zelfstudie [Aan de slag met Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="09acf-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

## <span data-ttu-id="09acf-112"><a name="configure-caching"> </a>Een bewerking voor opslaan in cache configureren</span><span class="sxs-lookup"><span data-stu-id="09acf-112"><a name="configure-caching"> </a>Configure an operation for caching</span></span>
<span data-ttu-id="09acf-113">In deze stap controleert u de cache-instellingen van de bewerking **GET Resource (in cache)** van de voorbeeld-Echo-API.</span><span class="sxs-lookup"><span data-stu-id="09acf-113">In this step, you will review the caching settings of the **GET Resource (cached)** operation of the sample Echo API.</span></span>

> [!NOTE]
> <span data-ttu-id="09acf-114">Elk service-exemplaar van API Management wordt al geconfigureerd geleverd met een Echo-API die kan worden gebruikt om te experimenteren met API Management en hier meer over te leren.</span><span class="sxs-lookup"><span data-stu-id="09acf-114">Each API Management service instance comes preconfigured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="09acf-115">Zie [Aan de slag met Azure API Management][Get started with Azure API Management] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="09acf-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span></span>
> 
> 

<span data-ttu-id="09acf-116">Als u aan de slag wilt gaan, klikt u op **Publicatieportal** in Azure Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="09acf-116">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="09acf-117">Hiermee gaat u naar de publicatieportal van API Management.</span><span class="sxs-lookup"><span data-stu-id="09acf-117">This takes you to the API Management publisher portal.</span></span>

![Publicatieportal][api-management-management-console]

<span data-ttu-id="09acf-119">Klik op **API's** in het menu **API Management** aan de linkerkant en klik vervolgens op **Echo-API**.</span><span class="sxs-lookup"><span data-stu-id="09acf-119">Click **APIs** from the **API Management** menu on the left, and then click **Echo API**.</span></span>

![Echo-API][api-management-echo-api]

<span data-ttu-id="09acf-121">Klik op het tabblad **Bewerkingen** en klik vervolgens op de bewerking **GET Resource (in cache)** in de lijst **Bewerkingen**.</span><span class="sxs-lookup"><span data-stu-id="09acf-121">Click the **Operations** tab, and then click the **GET Resource (cached)** operation from the **Operations** list.</span></span>

![Bewerkingen Echo-API][api-management-echo-api-operations]

<span data-ttu-id="09acf-123">Klik op het tabblad **Opslaan in cache** om de cache-instellingen voor deze bewerking te bekijken.</span><span class="sxs-lookup"><span data-stu-id="09acf-123">Click the **Caching** tab to view the caching settings for this operation.</span></span>

![Tabblad Opslaan in cache][api-management-caching-tab]

<span data-ttu-id="09acf-125">Als u opslaan in cache wilt inschakelen voor een bewerking, schakelt u het selectievakje **Inschakelen** in.</span><span class="sxs-lookup"><span data-stu-id="09acf-125">To enable caching for an operation, select the **Enable** check box.</span></span> <span data-ttu-id="09acf-126">In dit voorbeeld is opslaan in cache ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="09acf-126">In this example, caching is enabled.</span></span>

<span data-ttu-id="09acf-127">Elk bewerkingsantwoord heeft een sleutel, op basis van de waarden in de velden **Variëren op queryreeksparameters** en **Variëren op headers**.</span><span class="sxs-lookup"><span data-stu-id="09acf-127">Each operation response is keyed, based on the values in the **Vary by query string parameters** and **Vary by headers** fields.</span></span> <span data-ttu-id="09acf-128">Als u meerdere antwoorden in de cache wilt opslaan op basis van queryreeksparameters of headers, kunt u deze configureren in deze twee velden.</span><span class="sxs-lookup"><span data-stu-id="09acf-128">If you want to cache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span></span>

<span data-ttu-id="09acf-129">Met **Duur** wordt het vervalinterval opgegeven van de antwoorden in de cache.</span><span class="sxs-lookup"><span data-stu-id="09acf-129">**Duration** specifies the expiration interval of the cached responses.</span></span> <span data-ttu-id="09acf-130">In dit voorbeeld is het interval **3600** seconden, dat gelijk is aan één uur.</span><span class="sxs-lookup"><span data-stu-id="09acf-130">In this example, the interval is **3600** seconds, which is equivalent to one hour.</span></span>

<span data-ttu-id="09acf-131">Met de cacheconfiguratie in dit voorbeeld wordt met de eerste aanvraag voor de bewerking **GET Resource (in cache)** een antwoord geretourneerd van de back-endservice.</span><span class="sxs-lookup"><span data-stu-id="09acf-131">Using the caching configuration in this example, the first request to the **GET Resource (cached)** operation returns a response from the backend service.</span></span> <span data-ttu-id="09acf-132">Dit antwoord wordt in de cache opgeslagen, met een sleutel per de opgegeven headers en querytekenreeksparameters.</span><span class="sxs-lookup"><span data-stu-id="09acf-132">This response will be cached, keyed by the specified headers and query string parameters.</span></span> <span data-ttu-id="09acf-133">Voor volgende aanroepen voor de bewerking, met overeenkomende parameters, wordt het antwoord geretourneerd dat in de cache is opgeslagen, tot het cacheduurinterval is verlopen.</span><span class="sxs-lookup"><span data-stu-id="09acf-133">Subsequent calls to the operation, with matching parameters, will have the cached response returned, until the cache duration interval has expired.</span></span>

## <span data-ttu-id="09acf-134"><a name="caching-policies"> </a>De cachebeleidsregels controleren</span><span class="sxs-lookup"><span data-stu-id="09acf-134"><a name="caching-policies"> </a>Review the caching policies</span></span>
<span data-ttu-id="09acf-135">In deze stap controleert u de cache-instellingen voor de bewerking **GET Resource (in cache)** van de voorbeeld-Echo-API.</span><span class="sxs-lookup"><span data-stu-id="09acf-135">In this step, you review the caching settings for the **GET Resource (cached)** operation of the sample Echo API.</span></span>

<span data-ttu-id="09acf-136">Wanneer er cache-instellingen zijn geconfigureerd voor een bewerking op het tabblad **Opslaan in cache**, worden cachebeleidsregels toegevoegd voor de bewerking.</span><span class="sxs-lookup"><span data-stu-id="09acf-136">When caching settings are configured for an operation on the **Caching** tab, caching policies are added for the operation.</span></span> <span data-ttu-id="09acf-137">Deze beleidsregels kunnen worden bekeken en bewerkt in de beleidseditor.</span><span class="sxs-lookup"><span data-stu-id="09acf-137">These policies can be viewed and edited in the policy editor.</span></span>

<span data-ttu-id="09acf-138">Klik op **Beleidsregels** in het menu **API Management** menu aan de linkerkant en selecteer vervolgens **Echo-API / GET Resource (in cache)** in de vervolgkeuzelijst **Bewerking**.</span><span class="sxs-lookup"><span data-stu-id="09acf-138">Click **Policies** from the **API Management** menu on the left, and then select **Echo API / GET Resource (cached)** from the **Operation** drop-down list.</span></span>

![Bewerking beleidsbereik][api-management-operation-dropdown]

<span data-ttu-id="09acf-140">Hiermee worden de beleidsregels voor deze bewerking in de beleidseditor weergegeven.</span><span class="sxs-lookup"><span data-stu-id="09acf-140">This displays the policies for this operation in the policy editor.</span></span>

![Beleidseditor API Management][api-management-policy-editor]

<span data-ttu-id="09acf-142">De beleidsdefinitie voor deze bewerking bevat de beleidsregels waarmee de cacheconfiguratie wordt gedefinieerd die is gecontroleerd met het tabblad **Opslaan in cache** in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="09acf-142">The policy definition for this operation includes the policies that define the caching configuration that were reviewed using the **Caching** tab in the previous step.</span></span>

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
> <span data-ttu-id="09acf-143">Wijzigingen die via de beleidseditor in de cachebeleidsregels worden aangebracht, worden weergegeven op het tabblad **Opslaan in cache** van een bewerking en vice versa.</span><span class="sxs-lookup"><span data-stu-id="09acf-143">Changes made to the caching policies in the policy editor will be reflected on the **Caching** tab of an operation, and vice-versa.</span></span>
> 
> 

## <span data-ttu-id="09acf-144"><a name="test-operation"> </a>Een bewerking aanroepen en het opslaan in de cache testen</span><span class="sxs-lookup"><span data-stu-id="09acf-144"><a name="test-operation"> </a>Call an operation and test the caching</span></span>
<span data-ttu-id="09acf-145">Als u het opslaan in de cache in werking wilt zien, kunnen we de bewerking aanroepen vanuit de ontwikkelaarsportal.</span><span class="sxs-lookup"><span data-stu-id="09acf-145">To see the caching in action, we can call the operation from the developer portal.</span></span> <span data-ttu-id="09acf-146">Klik op **ontwikkelaarsportal** in het menu rechtsboven.</span><span class="sxs-lookup"><span data-stu-id="09acf-146">Click **Developer portal** in the top right menu.</span></span>

![Ontwikkelaarsportal][api-management-developer-portal-menu]

<span data-ttu-id="09acf-148">Klik op **API's** in het bovenste menu en selecteer **Echo-API**.</span><span class="sxs-lookup"><span data-stu-id="09acf-148">Click **APIs** in the top menu, and then select **Echo API**.</span></span>

![Echo-API][api-management-apis-echo-api]

> <span data-ttu-id="09acf-150">Als er slechts één API is geconfigureerd of zichtbaar is voor uw account, gaat u wanneer u op API's klikt rechtstreeks naar de bewerkingen voor die API.</span><span class="sxs-lookup"><span data-stu-id="09acf-150">If you have only one API configured or visible to your account, then clicking APIs takes you directly to the operations for that API.</span></span>
> 
> 

<span data-ttu-id="09acf-151">Selecteer de bewerking **GET Resource (in cache)** en klik op **Console openen**.</span><span class="sxs-lookup"><span data-stu-id="09acf-151">Select the **GET Resource (cached)** operation, and then click **Open Console**.</span></span>

![Console openen][api-management-open-console]

<span data-ttu-id="09acf-153">Met de console kunt u bewerkingen rechtstreeks vanuit de ontwikkelaarsportal aanroepen.</span><span class="sxs-lookup"><span data-stu-id="09acf-153">The console allows you to invoke operations directly from the developer portal.</span></span>

![Console][api-management-console]

<span data-ttu-id="09acf-155">Behoud de standaardwaarden voor **param1** en **param2**.</span><span class="sxs-lookup"><span data-stu-id="09acf-155">Keep the default values for **param1** and **param2**.</span></span>

<span data-ttu-id="09acf-156">Selecteer de gewenste sleutel in de vervolgkeuzelijst **subscription-key**.</span><span class="sxs-lookup"><span data-stu-id="09acf-156">Select the desired key from the **subscription-key** drop-down list.</span></span> <span data-ttu-id="09acf-157">Als uw account slechts één abonnement heeft, is de sleutel al geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="09acf-157">If your account has only one subscription, it will already be selected.</span></span>

<span data-ttu-id="09acf-158">Voer **sampleheader:value1** in het tekstvak **Aanvraagheaders** in.</span><span class="sxs-lookup"><span data-stu-id="09acf-158">Enter **sampleheader:value1** in the **Request headers** text box.</span></span>

<span data-ttu-id="09acf-159">Klik op **HTTP Get** en noteer de antwoordheaders.</span><span class="sxs-lookup"><span data-stu-id="09acf-159">Click **HTTP Get** and make a note of the response headers.</span></span>

<span data-ttu-id="09acf-160">Voer **sampleheader:value2** in het tekstvak **Aanvraagheaders** in en klik vervolgens op **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="09acf-160">Enter **sampleheader:value2** in the **Request headers** text box, and then click **HTTP Get**.</span></span>

<span data-ttu-id="09acf-161">Merk op dat de waarde van **sampleheader** nog steeds **value1** in het antwoord is.</span><span class="sxs-lookup"><span data-stu-id="09acf-161">Note that the value of **sampleheader** is still **value1** in the response.</span></span> <span data-ttu-id="09acf-162">Probeer een aantal verschillende waarden en merk op dat het antwoord in de cache van de eerste aanroep wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="09acf-162">Try some different values and note that the cached response from the first call is returned.</span></span>

<span data-ttu-id="09acf-163">Voer **25** in het veld **param2** in en klik vervolgens op **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="09acf-163">Enter **25** into the **param2** field, and then click **HTTP Get**.</span></span>

<span data-ttu-id="09acf-164">Merk op dat de waarde van **sampleheader** in het antwoord nu **value2** is.</span><span class="sxs-lookup"><span data-stu-id="09acf-164">Note that the value of **sampleheader** in the response is now **value2**.</span></span> <span data-ttu-id="09acf-165">Omdat de bewerkingsresultaten een sleutel per querytekenreeks hebben, is het vorige antwoord in de cache niet geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="09acf-165">Because the operation results are keyed by query string, the previous cached response was not returned.</span></span>

## <span data-ttu-id="09acf-166"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="09acf-166"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="09acf-167">Zie [Cachebeleidsregels][Caching policies] in [Naslaginformatie over beleid voor API Management][API Management policy reference] voor meer informatie over cachebeleidsregels.</span><span class="sxs-lookup"><span data-stu-id="09acf-167">For more information about caching policies, see [Caching policies][Caching policies] in the [API Management policy reference][API Management policy reference].</span></span>
* <span data-ttu-id="09acf-168">Zie [Aangepast opslaan in cache in Azure API Management](api-management-sample-cache-by-key.md) voor informatie over het opslaan van items in de cache per sleutel met behulp van beleidsexpressies.</span><span class="sxs-lookup"><span data-stu-id="09acf-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>

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


[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review the caching policies]: #caching-policies
[Call an operation and test the caching]: #test-operation
[Next steps]: #next-steps
