---
title: Het maken en een product publiceren in Azure API Management
description: Informatie over het maken en publiceren van producten in Azure API Management.
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
ms.openlocfilehash: 73bf4451ba1b71807e22440beecc73a7e8045c5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-publish-a-product-in-azure-api-management"></a><span data-ttu-id="a6a63-103">Het maken en een product publiceren in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="a6a63-103">How to create and publish a product in Azure API Management</span></span>
<span data-ttu-id="a6a63-104">In Azure API Management zijn een product bevat een of meer API's, evenals een gebruiksquotum en de gebruiksvoorwaarden.</span><span class="sxs-lookup"><span data-stu-id="a6a63-104">In Azure API Management, a product contains one or more APIs as well as a usage quota and the terms of use.</span></span> <span data-ttu-id="a6a63-105">Zodra een product is gepubliceerd, kunnen ontwikkelaars abonneren op het product en begint met het gebruik van API's van het product.</span><span class="sxs-lookup"><span data-stu-id="a6a63-105">Once a product is published, developers can subscribe to the product and begin to use the product's APIs.</span></span> <span data-ttu-id="a6a63-106">Het onderwerp bevat een handleiding voor het maken van een product, het toevoegen van een API en het publiceren van het voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="a6a63-106">The topic provides a guide to creating a product, adding an API, and publishing it for developers.</span></span>

## <span data-ttu-id="a6a63-107"><a name="create-product"></a>Een product maken</span><span class="sxs-lookup"><span data-stu-id="a6a63-107"><a name="create-product"> </a>Create a product</span></span>
<span data-ttu-id="a6a63-108">Bewerkingen zijn toegevoegd en geconfigureerd voor een API in de publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="a6a63-108">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="a6a63-109">Voor toegang tot de publicatieportal bevindt, klikt u op **publicatieportal** in de Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="a6a63-109">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Publicatieportal][api-management-management-console]

> <span data-ttu-id="a6a63-111">Als u nog geen service-exemplaar van API Management hebt gemaakt, raadpleegt u [Service-exemplaar van API Management maken][Create an API Management service instance] in de zelfstudie [Aan de slag met Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="a6a63-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="a6a63-112">Klik op **producten** in het menu aan de linkerkant om weer te geven de **producten** pagina en klik op **Product toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a6a63-112">Click on **Products** in the menu on the left to display the **Products** page, and click **Add Product**.</span></span>

![Producten][api-management-products]

![Nieuw product][api-management-add-new-product]

<span data-ttu-id="a6a63-115">Voer een beschrijvende naam voor het product in de **naam** veld en een beschrijving van het product in de **beschrijving** veld.</span><span class="sxs-lookup"><span data-stu-id="a6a63-115">Enter a descriptive name for the product in the **Name** field and a description of the product in the **Description** field.</span></span>

<span data-ttu-id="a6a63-116">Producten in API Management kunnen worden **Open** of **beveiligde**.</span><span class="sxs-lookup"><span data-stu-id="a6a63-116">Products in API Management can be **Open** or **Protected**.</span></span> <span data-ttu-id="a6a63-117">Voor beveiligde producten is een abonnement nodig voordat ze kunnen worden gebruikt, terwijl open producten zonder abonnement kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a6a63-117">Protected products must be subscribed to before they can be used, while open products can be used without a subscription.</span></span> <span data-ttu-id="a6a63-118">Controleer **abonnement vereisen** voor het maken van een beveiligd product waarvoor een abonnement.</span><span class="sxs-lookup"><span data-stu-id="a6a63-118">Check **Require subscription** to create a protected product that requires a subscription.</span></span> <span data-ttu-id="a6a63-119">Dit is de standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="a6a63-119">This is the default setting.</span></span>

<span data-ttu-id="a6a63-120">Controleer **goedkeuring abonnement vereisen** als u wilt dat een beheerder om te bekijken en accepteren of weigeren abonnementspogingen voor dit product.</span><span class="sxs-lookup"><span data-stu-id="a6a63-120">Check **Require subscription approval** if you want an administrator to review and accept or reject subscription attempts to this product.</span></span> <span data-ttu-id="a6a63-121">Als het selectievakje uitgeschakeld is, worden abonnementspogingen automatisch goedgekeurd.</span><span class="sxs-lookup"><span data-stu-id="a6a63-121">If the box is unchecked, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="a6a63-122">Zie voor meer informatie over abonnementen [abonnees van een product weergeven][View subscribers to a product].</span><span class="sxs-lookup"><span data-stu-id="a6a63-122">For more information on subscriptions, see [View subscribers to a product][View subscribers to a product].</span></span>

<span data-ttu-id="a6a63-123">Als u wilt toestaan dat ontwikkelaarsaccounts meerdere keren naar het product, Controleer de **meerdere abonnementen toestaan** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="a6a63-123">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box.</span></span> <span data-ttu-id="a6a63-124">Als dit selectievakje niet is ingeschakeld, kan elke ontwikkelaarsaccount slechts één keer aan het product abonneren.</span><span class="sxs-lookup"><span data-stu-id="a6a63-124">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

![Onbeperkte meerdere abonnementen][api-management-unlimited-multiple-subscriptions]

<span data-ttu-id="a6a63-126">Beperk het aantal meerdere gelijktijdige abonnementen, Controleer de **beperken het aantal gelijktijdige abonnementen op** selectievakje en voert u de limiet voor het abonnement.</span><span class="sxs-lookup"><span data-stu-id="a6a63-126">To limit the count of multiple simultaneous subscriptions, check the **Limit number of simultaneous subscriptions to** check box and enter the subscription limit.</span></span> <span data-ttu-id="a6a63-127">Gelijktijdige abonnementen zijn in het volgende voorbeeld wordt beperkt tot vier keer per developer-account.</span><span class="sxs-lookup"><span data-stu-id="a6a63-127">In the following example, simultaneous subscriptions are limited to four per developer account.</span></span>

![Vier meerdere abonnementen][api-management-four-multiple-subscriptions]

<span data-ttu-id="a6a63-129">Nadat alle productopties voor nieuw zijn geconfigureerd, klikt u op **opslaan** voor het maken van het nieuwe product.</span><span class="sxs-lookup"><span data-stu-id="a6a63-129">Once all new product options are configured, click **Save** to create the new product.</span></span>

![Producten][api-management-products-page]

> <span data-ttu-id="a6a63-131">Standaard nieuwe producten zijn niet gepubliceerd en zijn alleen zichtbaar voor de **beheerders** groep.</span><span class="sxs-lookup"><span data-stu-id="a6a63-131">By default new products are unpublished, and are visible only to the  **Administrators** group.</span></span>
> 
> 

<span data-ttu-id="a6a63-132">Voor het configureren van een product, klikt u op de naam van het product in de **producten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a6a63-132">To configure a product, click on the product name in the **Products** tab.</span></span>

## <span data-ttu-id="a6a63-133"><a name="add-apis"></a>API's toevoegen aan een product</span><span class="sxs-lookup"><span data-stu-id="a6a63-133"><a name="add-apis"> </a>Add APIs to a product</span></span>
<span data-ttu-id="a6a63-134">De **producten** pagina bevat vier koppelingen voor de configuratie: **samenvatting**, **instellingen**, **zichtbaarheid**, en **abonnees**.</span><span class="sxs-lookup"><span data-stu-id="a6a63-134">The **Products** page contains four links for configuration: **Summary**, **Settings**, **Visibility**, and **Subscribers**.</span></span> <span data-ttu-id="a6a63-135">De **samenvatting** tabblad kunt u API's toevoegen en publiceren of ongedaan maken van een product is.</span><span class="sxs-lookup"><span data-stu-id="a6a63-135">The **Summary** tab is where you can add APIs and publish or unpublish a product.</span></span>

![Samenvatting][api-management-new-product-summary]

<span data-ttu-id="a6a63-137">Voordat het publiceren van uw product moet u een of meer API's toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a6a63-137">Before publishing your product you need to add one or more APIs.</span></span> <span data-ttu-id="a6a63-138">Om dit te doen, klikt u op **API toevoegen aan product**.</span><span class="sxs-lookup"><span data-stu-id="a6a63-138">To do this, click **Add API to product**.</span></span>

![API's toevoegen][api-management-add-apis-to-product]

<span data-ttu-id="a6a63-140">Selecteer de gewenste API's en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a6a63-140">Select the desired APIs and click **Save**.</span></span>

## <span data-ttu-id="a6a63-141"><a name="add-description"></a>Beschrijvende informatie toevoegen aan een product</span><span class="sxs-lookup"><span data-stu-id="a6a63-141"><a name="add-description"> </a>Add descriptive information to a product</span></span>
<span data-ttu-id="a6a63-142">De **instellingen** tabblad kunt u gedetailleerde informatie over het product zoals het doel en de API's die u toegang tot krijgt andere nuttige informatie opgeven.</span><span class="sxs-lookup"><span data-stu-id="a6a63-142">The **Settings** tab allows you to provide detailed information about the product such as its purpose, the APIs it provides access to, and other useful information.</span></span> <span data-ttu-id="a6a63-143">De inhoud is gericht op de ontwikkelaars die aanroepen van de API en kunnen worden geschreven in tekst zonder opmaak of HTML-opmaak.</span><span class="sxs-lookup"><span data-stu-id="a6a63-143">The content is targeted at the developers that will be calling the API and can be written in plain text or HTML markup.</span></span>

![Productinstellingen][api-management-product-settings]

<span data-ttu-id="a6a63-145">Controleer **abonnement vereisen** voor het maken van een beveiligd product waarvoor een abonnement moet worden gebruikt of schakel het selectievakje uit om een open product die kan worden aangeroepen zonder een abonnement te maken.</span><span class="sxs-lookup"><span data-stu-id="a6a63-145">Check **Require subscription** to create a protected product that requires a subscription to be used, or clear the checkbox to create an open product that can be called without a subscription.</span></span>

<span data-ttu-id="a6a63-146">Selecteer **goedkeuring abonnement vereisen** desgewenst handmatig goedkeuren van alle aanvragen van de product-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a6a63-146">Select **Require subscription approval** if you want to manually approve all product subscription requests.</span></span> <span data-ttu-id="a6a63-147">Standaard worden alle product abonnementen automatisch verleend.</span><span class="sxs-lookup"><span data-stu-id="a6a63-147">By default all product subscriptions are granted automatically.</span></span>

<span data-ttu-id="a6a63-148">Als u wilt toestaan dat ontwikkelaarsaccounts meerdere keren naar het product, Controleer de **meerdere abonnementen toestaan** selectievakje en geef optioneel een limiet.</span><span class="sxs-lookup"><span data-stu-id="a6a63-148">To allow developer accounts to subscribe multiple times to the product, check the **Allow multiple subscriptions** check box and optionally specify a limit.</span></span> <span data-ttu-id="a6a63-149">Als dit selectievakje niet is ingeschakeld, kan elke ontwikkelaarsaccount slechts één keer aan het product abonneren.</span><span class="sxs-lookup"><span data-stu-id="a6a63-149">If this box is not checked, each developer account can subscribe only a single time to the product.</span></span>

<span data-ttu-id="a6a63-150">Vul eventueel de **gebruiksvoorwaarden** veld met een beschrijving van de gebruiksvoorwaarden voor het product welke abonnees accepteren moeten om te kunnen gebruiken van het product.</span><span class="sxs-lookup"><span data-stu-id="a6a63-150">Optionally fill in the **Terms of use** field describing the terms of use for the product which subscribers must accept in order to use the product.</span></span>

## <span data-ttu-id="a6a63-151"><a name="publish-product"></a>Een product publiceren</span><span class="sxs-lookup"><span data-stu-id="a6a63-151"><a name="publish-product"> </a>Publish a product</span></span>
<span data-ttu-id="a6a63-152">Voordat de API's in een product kan worden aangeroepen, moet het product worden gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="a6a63-152">Before the APIs in a product can be called, the product must be published.</span></span> <span data-ttu-id="a6a63-153">Op de **samenvatting** voor het product en klik op **publiceren**, en klik vervolgens op **Ja, publiceren** om te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="a6a63-153">On the **Summary** tab for the product, click **Publish**, and then click **Yes, publish it** to confirm.</span></span> <span data-ttu-id="a6a63-154">Een eerder gepubliceerde product als privé wilt maken, klikt u op **publicatie ongedaan maken**.</span><span class="sxs-lookup"><span data-stu-id="a6a63-154">To make a previously published product private, click **Unpublish**.</span></span>

![Product publiceren][api-management-publish-product]

## <span data-ttu-id="a6a63-156"><a name="make-visible"></a>Een product zichtbaar maken voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="a6a63-156"><a name="make-visible"> </a>Make a product visible to developers</span></span>
<span data-ttu-id="a6a63-157">De **zichtbaarheid** tabblad kunt u kiezen welke rollen kunnen zien van het product in de portal voor ontwikkelaars en zich abonneren op het product zijn.</span><span class="sxs-lookup"><span data-stu-id="a6a63-157">The **Visibility** tab allows you to choose which roles are able to see the product on the developer portal and subscribe to the product.</span></span>

![Zichtbaarheid van het product][api-management-product-visiblity]

<span data-ttu-id="a6a63-159">Als u wilt in- of uitschakelen van de zichtbaarheid van een product voor de ontwikkelaars in een groep, schakel of schakel het selectievakje naast de groep en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a6a63-159">To enable or disable visibility of a product for the developers in a group, check or uncheck the check box beside the group and then click **Save**.</span></span>

> <span data-ttu-id="a6a63-160">Zie voor meer informatie [maken en groepen gebruiken voor het beheren van de ontwikkelaarsaccounts in Azure API Management][How to create and use groups to manage developer accounts in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="a6a63-160">For more information, see [How to create and use groups to manage developer accounts in Azure API Management][How to create and use groups to manage developer accounts in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="a6a63-161"><a name="view-subscribers"></a>Abonnees van een product weergeven</span><span class="sxs-lookup"><span data-stu-id="a6a63-161"><a name="view-subscribers"> </a>View subscribers to a product</span></span>
<span data-ttu-id="a6a63-162">De **abonnees** tabblad bevat de ontwikkelaars die het product zijn geabonneerd.</span><span class="sxs-lookup"><span data-stu-id="a6a63-162">The **Subscribers** tab lists the developers who have subscribed to the product.</span></span> <span data-ttu-id="a6a63-163">De details en de instellingen voor elke ontwikkelaar kunnen worden bekeken door te klikken op de naam van de ontwikkelaar.</span><span class="sxs-lookup"><span data-stu-id="a6a63-163">The details and settings for each developer can be viewed by clicking on the developer's name.</span></span> <span data-ttu-id="a6a63-164">In dit voorbeeld hebt nog geen ontwikkelaars geabonneerd op het product.</span><span class="sxs-lookup"><span data-stu-id="a6a63-164">In this example no developers have yet subscribed to the product.</span></span>

![Ontwikkelaars][api-management-developer-list]

## <span data-ttu-id="a6a63-166"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a6a63-166"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="a6a63-167">Zodra de gewenste API's worden toegevoegd en het product gepubliceerd, kunnen ontwikkelaars abonneren op het product en begint met het aanroepen van de API's.</span><span class="sxs-lookup"><span data-stu-id="a6a63-167">Once the desired APIs are added and the product published, developers can subscribe to the product and begin to call the APIs.</span></span> <span data-ttu-id="a6a63-168">Zie voor een zelfstudie leert u hoe wordt deze items, evenals een geavanceerde productconfiguratie [maken en configureren van geavanceerde productinstellingen in Azure API Management][How create and configure advanced product settings in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="a6a63-168">For a tutorial that demonstrates these items as well as advanced product configuration see [How create and configure advanced product settings in Azure API Management][How create and configure advanced product settings in Azure API Management].</span></span>

<span data-ttu-id="a6a63-169">Zie voor meer informatie over het werken met producten in de volgende video.</span><span class="sxs-lookup"><span data-stu-id="a6a63-169">For more information about working with products, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs to a product]: #add-apis
[Add descriptive information to a product]: #add-description
[Publish a product]: #publish-product
[Make a product visible to developers]: #make-visible
[View subscribers to a product]: #view-subscribers
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


[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How to create and use groups to manage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
