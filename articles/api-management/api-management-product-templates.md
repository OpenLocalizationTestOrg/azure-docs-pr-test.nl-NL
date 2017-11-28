---
title: aaaProduct sjablonen in Azure API Management | Microsoft Docs
description: Meer informatie over hoe toocustomize Hallo inhoud van het product Hallo-pagina's in hello Azure API Management-portal voor ontwikkelaars.
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
ms.openlocfilehash: 60600299287aad87f9b621782ab5ceb866601d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="2907b-103">Productsjablonen in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="2907b-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="2907b-104">Azure API Management biedt dat u Hallo mogelijkheid toocustomize Hallo inhoud van developer portal-pagina's met behulp van een set van sjablonen die hun inhoud configureren.</span><span class="sxs-lookup"><span data-stu-id="2907b-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="2907b-105">Met behulp van [DotLiquid](http://dotliquidmarkup.org/) syntaxis en het Hallo-editor naar keuze, zoals [DotLiquid voor ontwerpers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), en een opgegeven set gelokaliseerde [resources String](api-management-template-resources.md#strings), [ De glyph-resources](api-management-template-resources.md#glyphs), en [pagina besturingselementen](api-management-page-controls.md), hebt u aanzienlijke flexibiliteit tooconfigure Hallo inhoud van het Hallo-pagina's naar wens met behulp van deze sjablonen.</span><span class="sxs-lookup"><span data-stu-id="2907b-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="2907b-106">Hallo-sjablonen in deze sectie kunt u toocustomize Hallo inhoud van het Hallo productpagina's in Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="2907b-106">hello templates in this section allow you toocustomize hello content of hello product pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="2907b-107">Lijst met producten</span><span class="sxs-lookup"><span data-stu-id="2907b-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="2907b-108">Product</span><span class="sxs-lookup"><span data-stu-id="2907b-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="2907b-109">Standaard-voorbeeldsjablonen zijn opgenomen in de volgende documentatie Hallo, maar onderwerp toochange vanwege toocontinuous verbeteringen zijn.</span><span class="sxs-lookup"><span data-stu-id="2907b-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="2907b-110">U kunt Hallo live standaardsjablonen in Hallo developer-portal door te navigeren toohello gewenst afzonderlijke sjablonen weergeven.</span><span class="sxs-lookup"><span data-stu-id="2907b-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="2907b-111">Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="2907b-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="2907b-112"><a name="ProductList"></a>Lijst met producten</span><span class="sxs-lookup"><span data-stu-id="2907b-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="2907b-113">Hallo **productlijst** sjabloon kunt u toocustomize Hallo hoofdtekst van de lijst productpagina Hallo in Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="2907b-113">hello **Product list** template allows you toocustomize hello body of hello product list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="2907b-114">![Lijst met producten](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="2907b-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="2907b-115">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="2907b-115">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="2907b-116">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="2907b-116">Controls</span></span>  
 <span data-ttu-id="2907b-117">Hallo `Product list` sjabloon mogelijk gebruikt u de volgende Hallo [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="2907b-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="2907b-118">besturingselement voor paginering</span><span class="sxs-lookup"><span data-stu-id="2907b-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="2907b-119">besturingselement voor zoeken</span><span class="sxs-lookup"><span data-stu-id="2907b-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="2907b-120">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="2907b-120">Data model</span></span>  
  
|<span data-ttu-id="2907b-121">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="2907b-121">Property</span></span>|<span data-ttu-id="2907b-122">Type</span><span class="sxs-lookup"><span data-stu-id="2907b-122">Type</span></span>|<span data-ttu-id="2907b-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2907b-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="2907b-124">Zoekresultaten oproepen</span><span class="sxs-lookup"><span data-stu-id="2907b-124">Paging</span></span>|<span data-ttu-id="2907b-125">[Wisselgeheugengebruik](api-management-template-data-model-reference.md#Paging) entiteit.</span><span class="sxs-lookup"><span data-stu-id="2907b-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="2907b-126">Hallo paginering informatie voor de verzameling van Hallo-producten.</span><span class="sxs-lookup"><span data-stu-id="2907b-126">hello paging information for hello products collection.</span></span>|  
|<span data-ttu-id="2907b-127">Filteren</span><span class="sxs-lookup"><span data-stu-id="2907b-127">Filtering</span></span>|<span data-ttu-id="2907b-128">[Filteren](api-management-template-data-model-reference.md#Filtering) entiteit.</span><span class="sxs-lookup"><span data-stu-id="2907b-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="2907b-129">Hallo filteren van gegevens voor Hallo producten pagina lijst.</span><span class="sxs-lookup"><span data-stu-id="2907b-129">hello filtering information for hello products list page.</span></span>|  
|<span data-ttu-id="2907b-130">Producten</span><span class="sxs-lookup"><span data-stu-id="2907b-130">Products</span></span>|<span data-ttu-id="2907b-131">Verzameling van [Product](api-management-template-data-model-reference.md#Product) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="2907b-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="2907b-132">Hallo producten zichtbaar toohello huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2907b-132">hello products visible toohello current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="2907b-133">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="2907b-133">Sample template data</span></span>  
  
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
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="2907b-134"><a name="Product"></a>Product</span><span class="sxs-lookup"><span data-stu-id="2907b-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="2907b-135">Hallo **Product** sjabloon kunt u toocustomize Hallo hoofdtekst van Hallo productpagina in Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="2907b-135">hello **Product** template allows you toocustomize hello body of hello product page in hello developer portal.</span></span>  
  
 <span data-ttu-id="2907b-136">![Developer portal productpagina](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="2907b-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="2907b-137">Standaardsjabloon</span><span class="sxs-lookup"><span data-stu-id="2907b-137">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="2907b-138">Besturingselementen</span><span class="sxs-lookup"><span data-stu-id="2907b-138">Controls</span></span>  
 <span data-ttu-id="2907b-139">Hallo `Product list` sjabloon mogelijk gebruikt u de volgende Hallo [pagina besturingselementen](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="2907b-139">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="2907b-140">abonneren knop</span><span class="sxs-lookup"><span data-stu-id="2907b-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="2907b-141">Gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="2907b-141">Data model</span></span>  
  
|<span data-ttu-id="2907b-142">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="2907b-142">Property</span></span>|<span data-ttu-id="2907b-143">Type</span><span class="sxs-lookup"><span data-stu-id="2907b-143">Type</span></span>|<span data-ttu-id="2907b-144">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2907b-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="2907b-145">Product</span><span class="sxs-lookup"><span data-stu-id="2907b-145">Product</span></span>|[<span data-ttu-id="2907b-146">Product</span><span class="sxs-lookup"><span data-stu-id="2907b-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="2907b-147">Hallo opgegeven product.</span><span class="sxs-lookup"><span data-stu-id="2907b-147">hello specified product.</span></span>|  
|<span data-ttu-id="2907b-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="2907b-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="2907b-149">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="2907b-149">boolean</span></span>|<span data-ttu-id="2907b-150">Hiermee wordt de huidige gebruiker Hallo geabonneerde toothis product.</span><span class="sxs-lookup"><span data-stu-id="2907b-150">Whether hello current user is subscribed toothis product.</span></span>|  
|<span data-ttu-id="2907b-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="2907b-151">SubscriptionState</span></span>|<span data-ttu-id="2907b-152">Aantal</span><span class="sxs-lookup"><span data-stu-id="2907b-152">number</span></span>|<span data-ttu-id="2907b-153">Hallo-status van het Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2907b-153">hello state of hello subscription.</span></span> <span data-ttu-id="2907b-154">Mogelijke statussen zijn:</span><span class="sxs-lookup"><span data-stu-id="2907b-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="2907b-155">-   `0 - suspended`– Hallo-abonnement is geblokkeerd en Hallo abonnee kan API's van Hallo product niet aanroepen.</span><span class="sxs-lookup"><span data-stu-id="2907b-155">-   `0 - suspended` – hello subscription is blocked, and hello subscriber cannot call any APIs of hello product.</span></span><br /><span data-ttu-id="2907b-156">-   `1 - active`– Hallo abonnement actief is.</span><span class="sxs-lookup"><span data-stu-id="2907b-156">-   `1 - active` – hello subscription is active.</span></span><br /><span data-ttu-id="2907b-157">-   `2 - expired`– Hallo-abonnement is bereikt de verloopdatum en is gedeactiveerd.</span><span class="sxs-lookup"><span data-stu-id="2907b-157">-   `2 - expired` – hello subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="2907b-158">-   `3 - submitted`– Hallo Abonnementaanvraag is gemaakt door de ontwikkelaar Hallo, maar is nog niet goedgekeurd of afgewezen.</span><span class="sxs-lookup"><span data-stu-id="2907b-158">-   `3 - submitted` – hello subscription request has been made by hello developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="2907b-159">-   `4 - rejected`– Hallo Abonnementaanvraag is geweigerd door een beheerder.</span><span class="sxs-lookup"><span data-stu-id="2907b-159">-   `4 - rejected` – hello subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="2907b-160">-   `5 - cancelled`– Hallo-abonnement is geannuleerd door Hallo ontwikkelaar of beheerder.</span><span class="sxs-lookup"><span data-stu-id="2907b-160">-   `5 - cancelled` – hello subscription has been cancelled by hello developer or administrator.</span></span>|  
|<span data-ttu-id="2907b-161">Limieten</span><span class="sxs-lookup"><span data-stu-id="2907b-161">Limits</span></span>|<span data-ttu-id="2907b-162">matrix</span><span class="sxs-lookup"><span data-stu-id="2907b-162">array</span></span>|<span data-ttu-id="2907b-163">Deze eigenschap is afgeschaft en mag niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2907b-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="2907b-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="2907b-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="2907b-165">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="2907b-165">boolean</span></span>|<span data-ttu-id="2907b-166">Of [delegering](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is ingeschakeld voor dit abonnement.</span><span class="sxs-lookup"><span data-stu-id="2907b-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="2907b-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="2907b-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="2907b-168">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="2907b-168">string</span></span>|<span data-ttu-id="2907b-169">Als delegering is ingeschakeld, gedelegeerd Hallo abonnement URL.</span><span class="sxs-lookup"><span data-stu-id="2907b-169">If delegation is enabled, hello delegated subscription URL.</span></span>|  
|<span data-ttu-id="2907b-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="2907b-170">IsAgreed</span></span>|<span data-ttu-id="2907b-171">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="2907b-171">boolean</span></span>|<span data-ttu-id="2907b-172">Als Hallo product voorwaarden heeft, of de huidige gebruiker Hallo heeft ingestemd toohello voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="2907b-172">If hello product has terms, whether hello current user has agreed toohello terms.</span></span>|  
|<span data-ttu-id="2907b-173">Abonnementen</span><span class="sxs-lookup"><span data-stu-id="2907b-173">Subscriptions</span></span>|<span data-ttu-id="2907b-174">Verzameling van [abonnement samenvatting](api-management-template-data-model-reference.md#SubscriptionSummary) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="2907b-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="2907b-175">Hallo abonnementen toohello product.</span><span class="sxs-lookup"><span data-stu-id="2907b-175">hello subscriptions toohello product.</span></span>|  
|<span data-ttu-id="2907b-176">API 's</span><span class="sxs-lookup"><span data-stu-id="2907b-176">Apis</span></span>|<span data-ttu-id="2907b-177">Verzameling van [API](api-management-template-data-model-reference.md#API) entiteiten.</span><span class="sxs-lookup"><span data-stu-id="2907b-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="2907b-178">Hallo API's in dit product.</span><span class="sxs-lookup"><span data-stu-id="2907b-178">hello APIs in this product.</span></span>|  
|<span data-ttu-id="2907b-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="2907b-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="2907b-180">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="2907b-180">boolean</span></span>|<span data-ttu-id="2907b-181">Hallo-huidige gebruiker wordt aangegeven of in aanmerking komende toosubscribe toothis product met inachtneming van toohello abonnementslimiet.</span><span class="sxs-lookup"><span data-stu-id="2907b-181">Whether hello current user is eligible toosubscribe toothis product with regard toohello subscription limit.</span></span>|  
|<span data-ttu-id="2907b-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="2907b-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="2907b-183">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="2907b-183">boolean</span></span>|<span data-ttu-id="2907b-184">Hiermee wordt de huidige gebruiker Hallo in aanmerking komende toosubscribe toothis product met inachtneming van toomultiple abonnementen of niet wordt toegestaan.</span><span class="sxs-lookup"><span data-stu-id="2907b-184">Whether hello current user is eligible toosubscribe toothis product with regard toomultiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="2907b-185">Voorbeeldgegevens voor sjabloon</span><span class="sxs-lookup"><span data-stu-id="2907b-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
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

## <a name="next-steps"></a><span data-ttu-id="2907b-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2907b-186">Next steps</span></span>
<span data-ttu-id="2907b-187">Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2907b-187">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
