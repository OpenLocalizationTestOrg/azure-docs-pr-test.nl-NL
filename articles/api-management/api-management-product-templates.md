---
title: Productsjablonen in Azure API Management | Microsoft Docs
description: Informatie over het aanpassen van de inhoud van de product-pagina's in de Azure API Management-portal voor ontwikkelaars.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 49f9254c-4c5f-4ed4-9c8d-798f44e805ee
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 9ddbb9860b437cb3e7334bdf5891f2fba1cffb76
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="cdb78-103">Productsjablonen in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="cdb78-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="cdb78-104">Azure API Management biedt de mogelijkheid voor het aanpassen van de inhoud van developer portal-pagina's met behulp van een set van sjablonen die hun inhoud configureren.</span><span class="sxs-lookup"><span data-stu-id="cdb78-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="cdb78-105">Met behulp van [DotLiquid](http://dotliquidmarkup.org/) syntaxis en de editor van uw keuze, zoals [DotLiquid voor ontwerpers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), en een opgegeven set gelokaliseerde [resources String](api-management-template-resources.md#strings), [Glyph-resources](api-management-template-resources.md#glyphs), en [pagina besturingselementen](api-management-page-controls.md), hebt u aanzienlijke flexibiliteit voor het configureren van de inhoud van de pagina's naar wens met behulp van deze sjablonen.</span><span class="sxs-lookup"><span data-stu-id="cdb78-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="cdb78-106">De sjablonen in deze sectie kunt u de inhoud van de product-pagina's in de ontwikkelaarsportal aanpassen.</span><span class="sxs-lookup"><span data-stu-id="cdb78-106">The templates in this section allow you to customize the content of the product pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="cdb78-107">Lijst met producten</span><span class="sxs-lookup"><span data-stu-id="cdb78-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="cdb78-108">Product</span><span class="sxs-lookup"><span data-stu-id="cdb78-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="cdb78-109">Standaard-voorbeeldsjablonen zijn opgenomen in de volgende documentatie, maar nog worden gewijzigd vanwege continu verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="cdb78-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="cdb78-110">U kunt de live standaardsjablonen weergeven in de ontwikkelaarsportal door te navigeren naar de gewenste afzonderlijke sjablonen.</span><span class="sxs-lookup"><span data-stu-id="cdb78-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="cdb78-111">Zie voor meer informatie over het werken met sjablonen [het aanpassen van de API Management portal voor ontwikkelaars met behulp van sjablonen](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="cdb78-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="cdb78-112"><a name="ProductList"></a>Lijst met producten</span><span class="sxs-lookup"><span data-stu-id="cdb78-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="cdb78-113">De **productlijst** sjabloon kunt u de hoofdtekst van de pagina van de lijst met product in de ontwikkelaarsportal aanpassen.</span><span class="sxs-lookup"><span data-stu-id="cdb78-113">The **Product list** template allows you to customize the body of the product list page in the developer portal.</span></span>  
  
 <span data-ttu-id="cdb78-114">![Lijst met producten](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="cdb78-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="cdb78-115">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="cdb78-115">Default template</span></span>  
  
```xml  
<search-control></search-control>  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if products.size > 0 %}  
    <ul class="list-unstyled">  
    {% for product in products %}  
        <li>  
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>  
            {{product.description}}  
        </li>     
    {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="cdb78-116">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="cdb78-116">Controls</span></span>  
 <span data-ttu-id="cdb78-117">De `Product list` sjabloon mogelijk gebruikt u de volgende [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="cdb78-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="cdb78-118">besturingselement voor paginering</span><span class="sxs-lookup"><span data-stu-id="cdb78-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="cdb78-119">besturingselement voor zoeken</span><span class="sxs-lookup"><span data-stu-id="cdb78-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="cdb78-120">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="cdb78-120">Data model</span></span>  
  
|<span data-ttu-id="cdb78-121">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="cdb78-121">Property</span></span>|<span data-ttu-id="cdb78-122">Type</span><span class="sxs-lookup"><span data-stu-id="cdb78-122">Type</span></span>|<span data-ttu-id="cdb78-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cdb78-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="cdb78-124">Zoekresultaten oproepen</span><span class="sxs-lookup"><span data-stu-id="cdb78-124">Paging</span></span>|<span data-ttu-id="cdb78-125">[Wisselgeheugengebruik](api-management-template-data-model-reference.md#Paging) entiteit.</span><span class="sxs-lookup"><span data-stu-id="cdb78-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="cdb78-126">De paginerings-informatie voor de verzameling producten.</span><span class="sxs-lookup"><span data-stu-id="cdb78-126">The paging information for the products collection.</span></span>|  
|<span data-ttu-id="cdb78-127">Filteren</span><span class="sxs-lookup"><span data-stu-id="cdb78-127">Filtering</span></span>|<span data-ttu-id="cdb78-128">[Filteren](api-management-template-data-model-reference.md#Filtering) entiteit.</span><span class="sxs-lookup"><span data-stu-id="cdb78-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="cdb78-129">De informatie filteren voor de pagina van de lijst met producten.</span><span class="sxs-lookup"><span data-stu-id="cdb78-129">The filtering information for the products list page.</span></span>|  
|<span data-ttu-id="cdb78-130">Producten</span><span class="sxs-lookup"><span data-stu-id="cdb78-130">Products</span></span>|<span data-ttu-id="cdb78-131">Verzameling van [Product](api-management-template-data-model-reference.md#Product) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="cdb78-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="cdb78-132">De producten die zichtbaar is voor de huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="cdb78-132">The products visible to the current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="cdb78-133">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="cdb78-133">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 2,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Filtering": {  
        "Pattern": null,  
        "Placeholder": "Search products"  
    },  
    "Products": [  
        {  
            "Id": "56f9445ffaf7560049060001",  
            "Title": "Starter",  
            "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="cdb78-134"><a name="Product"></a>Product</span><span class="sxs-lookup"><span data-stu-id="cdb78-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="cdb78-135">De **Product** sjabloon kunt u de hoofdtekst van de productpagina in de ontwikkelaarsportal aanpassen.</span><span class="sxs-lookup"><span data-stu-id="cdb78-135">The **Product** template allows you to customize the body of the product page in the developer portal.</span></span>  
  
 <span data-ttu-id="cdb78-136">![Developer portal productpagina](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="cdb78-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="cdb78-137">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="cdb78-137">Default template</span></span>  
  
```xml  
<h2>{{Product.Title}}</h2>  
<p>{{Product.Description}}</p>  
  
{% assign replaceString0 = '{0}' %}  
  
{% if Limits and Limits.size > 0 %}  
<h3>{% localized "ProductDetailsStrings|WebProductsUsageLimitsHeader"%}</h3>  
<ul>  
  {% for limit in Limits %}  
  <li>{{limit.DisplayName}}</li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if apis.size > 0 %}  
<p>  
  <b>  
    {% if apis.size == 1 %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockSingleApisCount" %}{% endcapture %}  
    {% else %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockMultipleApisCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture apisCount %}{{apis.size}}{% endcapture %}  
    {{ apisCountText | replace : replaceString0, apisCount }}  
  </b>  
</p>  
  
<ul>  
  {% for api in Apis %}  
  <li>  
    <a href="/docs/services/{{api.Id}}">{{api.Name}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if subscriptions.size > 0 %}  
<p>  
  <b>  
    {% if subscriptions.size == 1 %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockSingleSubscriptionsCount" %}{% endcapture %}  
    {% else %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockMultipleSubscriptionsCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture subscriptionsCount %}{{subscriptions.size}}{% endcapture %}  
    {{ subscriptionsCountText | replace : replaceString0, subscriptionsCount }}  
  </b>  
</p>  
  
<ul>  
  {% for subscription in subscriptions %}  
  <li>  
    <a href="/developer#{{subscription.Id}}">{{subscription.DisplayName}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
{% if CannotAddBecauseSubscriptionNumberLimitReached %}  
<b>{% localized "ProductDetailsStrings|TextblockSubscriptionLimitReached" %}</b>  
{% elsif CannotAddBecauseMultipleSubscriptionsNotAllowed == false %}  
<subscribe-button></subscribe-button>  
{% endif %}  
```  
  
### <a name="controls"></a><span data-ttu-id="cdb78-138">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="cdb78-138">Controls</span></span>  
 <span data-ttu-id="cdb78-139">De `Product list` sjabloon mogelijk gebruikt u de volgende [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="cdb78-139">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="cdb78-140">abonneren knop</span><span class="sxs-lookup"><span data-stu-id="cdb78-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="cdb78-141">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="cdb78-141">Data model</span></span>  
  
|<span data-ttu-id="cdb78-142">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="cdb78-142">Property</span></span>|<span data-ttu-id="cdb78-143">Type</span><span class="sxs-lookup"><span data-stu-id="cdb78-143">Type</span></span>|<span data-ttu-id="cdb78-144">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cdb78-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="cdb78-145">Product</span><span class="sxs-lookup"><span data-stu-id="cdb78-145">Product</span></span>|[<span data-ttu-id="cdb78-146">Product</span><span class="sxs-lookup"><span data-stu-id="cdb78-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="cdb78-147">Het opgegeven product.</span><span class="sxs-lookup"><span data-stu-id="cdb78-147">The specified product.</span></span>|  
|<span data-ttu-id="cdb78-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="cdb78-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="cdb78-149">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="cdb78-149">boolean</span></span>|<span data-ttu-id="cdb78-150">Hiermee wordt aangegeven of de huidige gebruiker is geabonneerd op dit product.</span><span class="sxs-lookup"><span data-stu-id="cdb78-150">Whether the current user is subscribed to this product.</span></span>|  
|<span data-ttu-id="cdb78-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="cdb78-151">SubscriptionState</span></span>|<span data-ttu-id="cdb78-152">Aantal</span><span class="sxs-lookup"><span data-stu-id="cdb78-152">number</span></span>|<span data-ttu-id="cdb78-153">De status van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="cdb78-153">The state of the subscription.</span></span> <span data-ttu-id="cdb78-154">Mogelijke statussen zijn:</span><span class="sxs-lookup"><span data-stu-id="cdb78-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="cdb78-155">-   `0 - suspended`– het abonnement is geblokkeerd en de abonnee kan API's van het product niet aanroepen.</span><span class="sxs-lookup"><span data-stu-id="cdb78-155">-   `0 - suspended` – the subscription is blocked, and the subscriber cannot call any APIs of the product.</span></span><br /><span data-ttu-id="cdb78-156">-   `1 - active`– het abonnement actief is.</span><span class="sxs-lookup"><span data-stu-id="cdb78-156">-   `1 - active` – the subscription is active.</span></span><br /><span data-ttu-id="cdb78-157">-   `2 - expired`– het abonnement is bereikt de verloopdatum en is gedeactiveerd.</span><span class="sxs-lookup"><span data-stu-id="cdb78-157">-   `2 - expired` – the subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="cdb78-158">-   `3 - submitted`– de Abonnementaanvraag is gemaakt door de ontwikkelaar, maar is nog niet goedgekeurd of afgewezen.</span><span class="sxs-lookup"><span data-stu-id="cdb78-158">-   `3 - submitted` – the subscription request has been made by the developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="cdb78-159">-   `4 - rejected`– de Abonnementaanvraag is geweigerd door een beheerder.</span><span class="sxs-lookup"><span data-stu-id="cdb78-159">-   `4 - rejected` – the subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="cdb78-160">-   `5 - cancelled`– het abonnement is geannuleerd door de ontwikkelaar of beheerder.</span><span class="sxs-lookup"><span data-stu-id="cdb78-160">-   `5 - cancelled` – the subscription has been cancelled by the developer or administrator.</span></span>|  
|<span data-ttu-id="cdb78-161">Limieten</span><span class="sxs-lookup"><span data-stu-id="cdb78-161">Limits</span></span>|<span data-ttu-id="cdb78-162">matrix</span><span class="sxs-lookup"><span data-stu-id="cdb78-162">array</span></span>|<span data-ttu-id="cdb78-163">Deze eigenschap is afgeschaft en mag niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cdb78-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="cdb78-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="cdb78-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="cdb78-165">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="cdb78-165">boolean</span></span>|<span data-ttu-id="cdb78-166">Of [delegering](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is ingeschakeld voor dit abonnement.</span><span class="sxs-lookup"><span data-stu-id="cdb78-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="cdb78-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="cdb78-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="cdb78-168">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="cdb78-168">string</span></span>|<span data-ttu-id="cdb78-169">Als delegering is ingeschakeld, de URL van de gedelegeerde abonnement.</span><span class="sxs-lookup"><span data-stu-id="cdb78-169">If delegation is enabled, the delegated subscription URL.</span></span>|  
|<span data-ttu-id="cdb78-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="cdb78-170">IsAgreed</span></span>|<span data-ttu-id="cdb78-171">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="cdb78-171">boolean</span></span>|<span data-ttu-id="cdb78-172">Als het product termen, zijn ongeacht of de huidige gebruiker heeft ingestemd met de voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="cdb78-172">If the product has terms, whether the current user has agreed to the terms.</span></span>|  
|<span data-ttu-id="cdb78-173">Abonnementen</span><span class="sxs-lookup"><span data-stu-id="cdb78-173">Subscriptions</span></span>|<span data-ttu-id="cdb78-174">Verzameling van [abonnement samenvatting](api-management-template-data-model-reference.md#SubscriptionSummary) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="cdb78-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="cdb78-175">De abonnementen aan het product.</span><span class="sxs-lookup"><span data-stu-id="cdb78-175">The subscriptions to the product.</span></span>|  
|<span data-ttu-id="cdb78-176">API 's</span><span class="sxs-lookup"><span data-stu-id="cdb78-176">Apis</span></span>|<span data-ttu-id="cdb78-177">Verzameling van [API](api-management-template-data-model-reference.md#API) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="cdb78-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="cdb78-178">De API's in dit product.</span><span class="sxs-lookup"><span data-stu-id="cdb78-178">The APIs in this product.</span></span>|  
|<span data-ttu-id="cdb78-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="cdb78-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="cdb78-180">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="cdb78-180">boolean</span></span>|<span data-ttu-id="cdb78-181">Hiermee wordt aangegeven of de huidige gebruiker komt in aanmerking voor een abonnement voor dit product met betrekking tot de limiet voor het abonnement.</span><span class="sxs-lookup"><span data-stu-id="cdb78-181">Whether the current user is eligible to subscribe to this product with regard to the subscription limit.</span></span>|  
|<span data-ttu-id="cdb78-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="cdb78-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="cdb78-183">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="cdb78-183">boolean</span></span>|<span data-ttu-id="cdb78-184">Hiermee wordt aangegeven of de huidige gebruiker komt in aanmerking voor een abonnement voor dit product met betrekking tot meerdere abonnementen of niet wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="cdb78-184">Whether the current user is eligible to subscribe to this product with regard to multiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="cdb78-185">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="cdb78-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
        "Terms": "",  
        "ProductState": 1,  
        "AllowMultipleSubscriptions": false,  
        "MultipleSubscriptionsCount": 1  
    },  
    "IsDeveloperSubscribed": true,  
    "SubscriptionState": 1,  
    "Limits": [],  
    "DelegatedSubscriptionEnabled": false,  
    "DelegatedSubscriptionUrl": null,  
    "IsAgreed": false,  
    "Subscriptions": [  
        {  
            "Id": "56f9445ffaf7560049070001",  
            "DisplayName": "Starter  (default)"  
        }  
    ],  
    "Apis": [  
        {  
            "id": "56f9445ffaf7560049040001",  
            "name": "Echo API",  
            "description": null,  
            "serviceUrl": "http://echoapi.cloudapp.net/api",  
            "path": "echo",  
            "protocols": [  
                2  
            ],  
            "authenticationSettings": null,  
            "subscriptionKeyParameterNames": null  
        }  
    ],  
    "CannotAddBecauseSubscriptionNumberLimitReached": false,  
    "CannotAddBecauseMultipleSubscriptionsNotAllowed": true  
}  
```

## <a name="next-steps"></a><span data-ttu-id="cdb78-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cdb78-186">Next steps</span></span>
<span data-ttu-id="cdb78-187">Zie voor meer informatie over het werken met sjablonen [het aanpassen van de API Management portal voor ontwikkelaars met behulp van sjablonen](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="cdb78-187">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>