---
title: aaaHow toocreate en een product publiceren in Azure API Management
description: Meer informatie over hoe toocreate en producten publiceren in Azure API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f0a37f08b4e29ca68be9caec4c7604e3b4b6aaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="75d47-103">Hoe toocreate en een product publiceren in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="75d47-103">How toocreate and publish a product in Azure API Management</span></span>
<span data-ttu-id="75d47-104">In Azure API Management zijn een product bevat een of meer API's, evenals een usage-quota's en Hallo gebruiksvoorwaarden.</span><span class="sxs-lookup"><span data-stu-id="75d47-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and hello terms of use.</span></span> <span data-ttu-id="75d47-105">Zodra een product is gepubliceerd, kunnen ontwikkelaars toohello product abonneren en begint toouse Hallo product API's.</span><span class="sxs-lookup"><span data-stu-id="75d47-105">Once a product is published, developers can subscribe toohello product and begin toouse hello product's APIs.</span></span> <span data-ttu-id="75d47-106">Hallo onderwerp bevat een handleiding toocreating een product, een API toevoegen en publiceren voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="75d47-106">hello topic provides a guide toocreating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="75d47-107"><a name="create-product"></a>Een product maken</span><span class="sxs-lookup"><span data-stu-id="75d47-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="75d47-108">Bewerkingen worden toegevoegd en tooan API in de publicatieportal Hallo geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="75d47-108">Operations are added and configured tooan API in hello publisher portal.</span></span> <span data-ttu-id="75d47-109">tooaccess publisher en klik op Hallo **publicatieportal** in hello Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="75d47-109">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Publicatieportal][api-management-management-console]

> <span data-ttu-id="75d47-111">Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="75d47-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="75d47-112">Klik op **producten** in Hallo-menu op Hallo links toodisplay hello **producten** pagina en klik op **Product toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="75d47-112">Click on **Products** in hello menu on hello left toodisplay hello **Products** page, and click **Add Product**.</span></span>

![Producten][api-management-products]

![Nieuw product][api-management-add-new-product]

<span data-ttu-id="75d47-115">Voer een beschrijvende naam voor Hallo product in Hallo **naam** veld en een beschrijving van het product in Hallo Hallo **beschrijving** veld.</span><span class="sxs-lookup"><span data-stu-id="75d47-115">Enter a descriptive name for hello product in hello **Name** field and a description of hello product in hello **Description** field.</span></span>

<span data-ttu-id="75d47-116">Producten in API Management kunnen worden **Open** of **beveiligde**.</span><span class="sxs-lookup"><span data-stu-id="75d47-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="75d47-117">Beveiligde producten moet geabonneerde toobefore ze kunnen worden gebruikt, terwijl open producten zonder abonnement kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="75d47-117">Protected products must be subscribed toobefore they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="75d47-118">Controleer **abonnement vereisen** toocreate een beveiligd product waarvoor een abonnement.</span><span class="sxs-lookup"><span data-stu-id="75d47-118">Check **Require subscription** toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="75d47-119">Dit is de standaardinstelling Hallo.</span><span class="sxs-lookup"><span data-stu-id="75d47-119">This is hello default setting.</span></span>

<span data-ttu-id="75d47-120">Controleer **goedkeuring abonnement vereisen** als u wilt dat een beheerder tooreview en accepteren of weigeren abonnement toothis product probeert.</span><span class="sxs-lookup"><span data-stu-id="75d47-120">Check **Require subscription approval** if you want an administrator tooreview and accept or reject subscription attempts toothis product.</span></span> <span data-ttu-id="75d47-121">Als Hallo selectievakje uitgeschakeld is, worden abonnementspogingen automatisch goedgekeurd.</span><span class="sxs-lookup"><span data-stu-id="75d47-121">If hello box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="75d47-122">Zie voor meer informatie over abonnementen [weergave abonnees tooa product][View subscribers tooa product].</span><span class="sxs-lookup"><span data-stu-id="75d47-122">For more information on subscriptions, see [View subscribers tooa product][View subscribers tooa product].</span></span>

<span data-ttu-id="75d47-123">tooallow developer accounts toosubscribe meerdere keren toohello product, Controleer Hallo **meerdere abonnementen toestaan** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="75d47-123">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="75d47-124">Als dit selectievakje niet is ingeschakeld, kunt alleen een product voor één keer toohello zich abonneren elke developer-account.</span><span class="sxs-lookup"><span data-stu-id="75d47-124">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

![Onbeperkte meerdere abonnementen][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="75d47-126">toolimit hello telling van meerdere gelijktijdige abonnementen controleren Hallo **beperken het aantal gelijktijdige abonnementen op** selectievakje en Voer Hallo limiet voor het abonnement.</span><span class="sxs-lookup"><span data-stu-id="75d47-126">toolimit hello count of multiple simultaneous subscriptions, check hello **Limit number of simultaneous subscriptions to** check box and enter hello subscription limit.</span></span> <span data-ttu-id="75d47-127">Gelijktijdige abonnementen zijn in de Hallo voorbeeld te volgen, beperkt toofour per developer-account.</span><span class="sxs-lookup"><span data-stu-id="75d47-127">In hello following example, simultaneous subscriptions are limited toofour per developer account.</span></span>

![Vier meerdere abonnementen][api-management-four-multiple-subscriptions]

<span data-ttu-id="75d47-129">Nadat alle productopties voor nieuw zijn geconfigureerd, klikt u op **opslaan** toocreate Hallo nieuw product.</span><span class="sxs-lookup"><span data-stu-id="75d47-129">Once all new product options are configured, click **Save** toocreate hello new product.</span></span>

![Producten][api-management-products-page]

> <span data-ttu-id="75d47-131">Standaard worden nieuwe producten zijn niet gepubliceerd en zijn zichtbaar alleen toohello **beheerders** groep.</span><span class="sxs-lookup"><span data-stu-id="75d47-131">By default new products are unpublished, and are visible only toohello  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="75d47-132">tooconfigure een product, klikt u op Hallo productnaam in Hallo **producten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="75d47-132">tooconfigure a product, click on hello product name in hello **Products** tab.</span></span>

## <span data-ttu-id="75d47-133"><a name="add-apis"></a>Toevoegen-API's tooa product</span><span class="sxs-lookup"><span data-stu-id="75d47-133"><a name="add-apis"> </a>Add APIs tooa product</span></span>
<span data-ttu-id="75d47-134">Hallo **producten** pagina bevat vier koppelingen voor de configuratie: **samenvatting**, **instellingen**, **zichtbaarheid**, en  **Abonnees**.</span><span class="sxs-lookup"><span data-stu-id="75d47-134">hello **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="75d47-135">Hallo **samenvatting** tabblad kunt u API's toevoegen en publiceren of ongedaan maken van een product is.</span><span class="sxs-lookup"><span data-stu-id="75d47-135">hello **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![Samenvatting][api-management-new-product-summary]

<span data-ttu-id="75d47-137">Voordat het product publiceren moet u tooadd een of meer API's.</span><span class="sxs-lookup"><span data-stu-id="75d47-137">Before publishing your product you need tooadd one or more APIs.</span></span> <span data-ttu-id="75d47-138">toodo, klikt u op **API toevoegen tooproduct**.</span><span class="sxs-lookup"><span data-stu-id="75d47-138">toodo this, click **Add API tooproduct**.</span></span>

![API's toevoegen][api-management-add-apis-to-product]

<span data-ttu-id="75d47-140">Selecteer Hallo gewenst API's en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="75d47-140">Select hello desired APIs and click **Save**.</span></span>

## <span data-ttu-id="75d47-141"><a name="add-description"></a>Beschrijvende informatie tooa-product toevoegen</span><span class="sxs-lookup"><span data-stu-id="75d47-141"><a name="add-description"> </a>Add descriptive information tooa product</span></span>
<span data-ttu-id="75d47-142">Hallo **instellingen** tabblad kunt u tooprovide gedetailleerde informatie over Hallo product zoals het doel ervan, Hallo toegang tot biedt API's en andere nuttige informatie.</span><span class="sxs-lookup"><span data-stu-id="75d47-142">hello **Settings** tab allows you tooprovide detailed information about hello product such as its purpose, hello APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="75d47-143">Hallo-inhoud is gericht op Hallo-ontwikkelaars die aanroepen van Hallo API en kunnen worden geschreven in tekst zonder opmaak of HTML-opmaak.</span><span class="sxs-lookup"><span data-stu-id="75d47-143">hello content is targeted at hello developers that will be calling hello API and can be written in plain text or HTML markup.</span></span>

![Productinstellingen][api-management-product-settings]

<span data-ttu-id="75d47-145">Controleer **abonnement vereisen** toocreate een beveiligd product waarvoor een abonnement toobe gebruikte, of schakel Hallo selectievakje toocreate een open product dat kan worden aangeroepen zonder een abonnement.</span><span class="sxs-lookup"><span data-stu-id="75d47-145">Check **Require subscription** toocreate a protected product that requires a subscription toobe used, or clear hello checkbox toocreate an open product that can be called without a subscription.</span></span>

<span data-ttu-id="75d47-146">Selecteer **goedkeuring abonnement vereisen** als u wilt dat toomanually alle product abonnement aanvragen goedkeuren.</span><span class="sxs-lookup"><span data-stu-id="75d47-146">Select **Require subscription approval** if you want toomanually approve all product subscription requests.</span></span> <span data-ttu-id="75d47-147">Standaard worden alle product abonnementen automatisch verleend.</span><span class="sxs-lookup"><span data-stu-id="75d47-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="75d47-148">tooallow developer accounts toosubscribe meerdere keren toohello product, Controleer Hallo **meerdere abonnementen toestaan** selectievakje en geef optioneel een limiet.</span><span class="sxs-lookup"><span data-stu-id="75d47-148">tooallow developer accounts toosubscribe multiple times toohello product, check hello **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="75d47-149">Als dit selectievakje niet is ingeschakeld, kunt alleen een product voor één keer toohello zich abonneren elke developer-account.</span><span class="sxs-lookup"><span data-stu-id="75d47-149">If this box is not checked, each developer account can subscribe only a single time toohello product.</span></span>

<span data-ttu-id="75d47-150">Vul eventueel Hallo **gebruiksvoorwaarden** veld Hallo gebruiksvoorwaarden voor Hallo product die abonnees in volgorde toouse Hallo product moeten accepteren.</span><span class="sxs-lookup"><span data-stu-id="75d47-150">Optionally fill in hello **Terms of use** field describing hello terms of use for hello product which subscribers must accept in order toouse hello product.</span></span>

## <span data-ttu-id="75d47-151"><a name="publish-product"></a>Een product publiceren</span><span class="sxs-lookup"><span data-stu-id="75d47-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="75d47-152">Voordat Hallo API's in een product kan worden aangeroepen, moet Hallo product worden gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="75d47-152">Before hello APIs in a product can be called, hello product must be published.</span></span> <span data-ttu-id="75d47-153">Op Hallo **samenvatting** voor Hallo product en klik op **publiceren**, en klik vervolgens op **Ja, publiceren** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="75d47-153">On hello **Summary** tab for hello product, click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span> <span data-ttu-id="75d47-154">toomake een persoonlijk eerder gepubliceerde product, klikt u op **publicatie ongedaan maken**.</span><span class="sxs-lookup"><span data-stu-id="75d47-154">toomake a previously published product private, click **Unpublish**.</span></span>

![Product publiceren][api-management-publish-product]

## <span data-ttu-id="75d47-156"><a name="make-visible"></a>Maken van een product zichtbaar toodevelopers</span><span class="sxs-lookup"><span data-stu-id="75d47-156"><a name="make-visible"> </a>Make a product visible toodevelopers</span></span>
<span data-ttu-id="75d47-157">Hallo **zichtbaarheid** tabblad kunt u toochoose welke functies kunnen toosee Hallo product op Hallo-portal voor ontwikkelaars en toohello product abonneren.</span><span class="sxs-lookup"><span data-stu-id="75d47-157">hello **Visibility** tab allows you toochoose which roles are able toosee hello product on hello developer portal and subscribe toohello product.</span></span>

![Zichtbaarheid van het product][api-management-product-visiblity]

<span data-ttu-id="75d47-159">controleren of schakel het selectievakje Hallo naast Hallo groep en klik vervolgens op tooenable of schakelt u de zichtbaarheid van een product voor ontwikkelaars Hallo in een groep **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="75d47-159">tooenable or disable visibility of a product for hello developers in a group, check or uncheck hello check box beside hello group and then click **Save**.</span></span>

> <span data-ttu-id="75d47-160">Zie voor meer informatie [hoe toocreate en gebruik groepen toomanage developer accounts in Azure API Management][How toocreate and use groups toomanage developer accounts in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="75d47-160">For more information, see [How toocreate and use groups toomanage developer accounts in Azure API Management][How toocreate and use groups toomanage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="75d47-161"><a name="view-subscribers"></a>Abonnees tooa-product weergeven</span><span class="sxs-lookup"><span data-stu-id="75d47-161"><a name="view-subscribers"> </a>View subscribers tooa product</span></span>
<span data-ttu-id="75d47-162">Hallo **abonnees** tabblad Hallo-ontwikkelaars die zijn geabonneerd toohello product bevat.</span><span class="sxs-lookup"><span data-stu-id="75d47-162">hello **Subscribers** tab lists hello developers who have subscribed toohello product.</span></span> <span data-ttu-id="75d47-163">Hallo kunnen-gegevens en instellingen voor elke ontwikkelaar worden bekeken door te klikken op Hallo ontwikkelaarshandleiding naam.</span><span class="sxs-lookup"><span data-stu-id="75d47-163">hello details and settings for each developer can be viewed by clicking on hello developer's name.</span></span> <span data-ttu-id="75d47-164">In dit voorbeeld hebben geen ontwikkelaars nog toohello product geabonneerd.</span><span class="sxs-lookup"><span data-stu-id="75d47-164">In this example no developers have yet subscribed toohello product.</span></span>

![Ontwikkelaars][api-management-developer-list]

## <span data-ttu-id="75d47-166"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="75d47-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="75d47-167">Hallo gewenste eenmaal API's toegevoegd en Hallo product is gepubliceerd, ontwikkelaars kunnen toohello product abonneren en beginnen met toocall Hallo API's.</span><span class="sxs-lookup"><span data-stu-id="75d47-167">Once hello desired APIs are added and hello product published, developers can subscribe toohello product and begin toocall hello APIs.</span></span> <span data-ttu-id="75d47-168">Zie voor een zelfstudie leert u hoe wordt deze items, evenals een geavanceerde productconfiguratie [maken en configureren van geavanceerde productinstellingen in Azure API Management][How create and configure advanced product settings in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="75d47-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="75d47-169">Zie voor meer informatie over het werken met producten Hallo video te volgen.</span><span class="sxs-lookup"><span data-stu-id="75d47-169">For more information about working with products, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs tooa product]: #add-apis
[Add descriptive information tooa product]: #add-description
[Publish a product]: #publish-product
[Make a product visible toodevelopers]: #make-visible
[View subscribers tooa product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: ./media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: ./media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: ./media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: ./media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: ./media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: ./media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: ./media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: ./media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: ./media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: ./media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How toocreate and use groups toomanage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
