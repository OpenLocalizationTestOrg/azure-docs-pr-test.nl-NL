---
title: Uw API beveiligen met Azure API Management | Microsoft Docs
description: Informatie over het beveiligen van uw API met beleidsregels voor quota en (frequentie)beperking.
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 5553bcb8f9fd38630f694151dc644a684266387c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a><span data-ttu-id="a31d4-103">Uw API beveiligen met frequentielimieten met behulp van Azure API Management</span><span class="sxs-lookup"><span data-stu-id="a31d4-103">Protect your API with rate limits using Azure API Management</span></span>
<span data-ttu-id="a31d4-104">In deze handleiding wordt getoond hoe eenvoudig het is om beveiliging toe te voegen voor uw back-end-API door frequentielimiet- en quotumbeleidsregels te configureren met Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="a31d4-104">This guide shows you how easy it is to add protection for your backend API by configuring rate limit and quota policies with Azure API Management.</span></span>

<span data-ttu-id="a31d4-105">In deze zelfstudie maakt u een API-product Gratis proefversie waarmee ontwikkelaars maximaal 10 aanroepen per minuut en maximaal 200 oproepen per week naar uw API kunnen doen met de beleidsregels [Aanroepfrequentie per abonnement beperken](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) en [Gebruiksquotum per abonnement instellen](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota).</span><span class="sxs-lookup"><span data-stu-id="a31d4-105">In this tutorial, you will create a "Free Trial" API product that allows developers to make up to 10 calls per minute and up to a maximum of 200 calls per week to your API using the [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="a31d4-106">Vervolgens publiceert u de API en test u het frequentielimietbeleid.</span><span class="sxs-lookup"><span data-stu-id="a31d4-106">You will then publish the API and test the rate limit policy.</span></span>

<span data-ttu-id="a31d4-107">Voor meer geavanceerde beperkingsscenario's met behulp van de beleidsregels [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) en [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) raadpleegt u [Geavanceerde aanvraagbeperking met Azure API Management](api-management-sample-flexible-throttling.md).</span><span class="sxs-lookup"><span data-stu-id="a31d4-107">For more advanced throttling scenarios using the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies, see [Advanced request throttling with Azure API Management](api-management-sample-flexible-throttling.md).</span></span>

## <span data-ttu-id="a31d4-108"><a name="create-product"> </a>Een product maken</span><span class="sxs-lookup"><span data-stu-id="a31d4-108"><a name="create-product"> </a>To create a product</span></span>
<span data-ttu-id="a31d4-109">In deze stap maakt u een product Gratis proefversie waarvoor geen abonnementsgoedkeuring is vereist.</span><span class="sxs-lookup"><span data-stu-id="a31d4-109">In this step, you will create a Free Trial product that does not require subscription approval.</span></span>

> [!NOTE]
> <span data-ttu-id="a31d4-110">Als u al een product hebt geconfigureerd en u dit wilt gebruiken voor deze zelfstudie, kunt u verder gaan naar [Aanroepfrequentielimiet- en quotumbeleidsregels configureren][Configure call rate limit and quota policies] en de zelfstudie vanaf daar volgen met uw product in plaats van het product Gratis proefversie.</span><span class="sxs-lookup"><span data-stu-id="a31d4-110">If you already have a product configured and want to use it for this tutorial, you can jump ahead to [Configure call rate limit and quota policies][Configure call rate limit and quota policies] and follow the tutorial from there using your product in place of the Free Trial product.</span></span>
> 
> 

<span data-ttu-id="a31d4-111">Als u aan de slag wilt gaan, klikt u op **Publicatieportal** in Azure Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="a31d4-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Publicatieportal][api-management-management-console]

> <span data-ttu-id="a31d4-113">Als u nog geen service-exemplaar van API Management hebt gemaakt, raadpleegt u [Service-exemplaar van API Management maken][Create an API Management service instance] in de zelfstudie [Uw eerste API beheren][Manage your first API in Azure API Management] in Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="a31d4-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Manage your first API in Azure API Management][Manage your first API in Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="a31d4-114">Klik op **Producten** in het menu **API Management** aan de linkerkant om de pagina **Producten** weer te geven.</span><span class="sxs-lookup"><span data-stu-id="a31d4-114">Click **Products** in the **API Management** menu on the left to display the **Products** page.</span></span>

![Product toevoegen][api-management-add-product]

<span data-ttu-id="a31d4-116">Klik op **Product toevoegen** om het dialoogvenster **Nieuw product toevoegen** weer te geven.</span><span class="sxs-lookup"><span data-stu-id="a31d4-116">Click **Add product** to display the **Add new product** dialog box.</span></span>

![Nieuw product toevoegen][api-management-new-product-window]

<span data-ttu-id="a31d4-118">Typ **Gratis proefversie** in het vak **Titel**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-118">In the **Title** box, type **Free Trial**.</span></span>

<span data-ttu-id="a31d4-119">Typ in het vak **Beschrijving** de volgende tekst: **Abonnees kunnen 10 aanroepen/minuut uitvoeren met maximaal 200 aanroepen/week, waarna toegang wordt geweigerd.**</span><span class="sxs-lookup"><span data-stu-id="a31d4-119">In the **Description** box, type the following text: **Subscribers will be able to run 10 calls/minute up to a maximum of 200 calls/week after which access is denied.**</span></span>

<span data-ttu-id="a31d4-120">Producten in API Management kunnen worden beveiligd of open zijn.</span><span class="sxs-lookup"><span data-stu-id="a31d4-120">Products in API Management can be protected or open.</span></span> <span data-ttu-id="a31d4-121">Voor beveiligde producten is een abonnement vereist voordat ze kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a31d4-121">Protected products must be subscribed to before they can be used.</span></span> <span data-ttu-id="a31d4-122">Open producten kunnen zonder abonnement worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a31d4-122">Open products can be used without a subscription.</span></span> <span data-ttu-id="a31d4-123">Zorg ervoor dat **Abonnement vereisen** is ingeschakeld voor het maken van een beveiligd product waarvoor een abonnement is vereist.</span><span class="sxs-lookup"><span data-stu-id="a31d4-123">Ensure that **Require subscription** is selected to create a protected product that requires a subscription.</span></span> <span data-ttu-id="a31d4-124">Dit is de standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="a31d4-124">This is the default setting.</span></span>

<span data-ttu-id="a31d4-125">Als u wilt dat een beheerder abonnementspogingen voor dit product beoordeelt en accepteert of weigert, schakelt u **Goedkeuring abonnement vereisen** in.</span><span class="sxs-lookup"><span data-stu-id="a31d4-125">If you want an administrator to review and accept or reject subscription attempts to this product, select **Require subscription approval**.</span></span> <span data-ttu-id="a31d4-126">Als het selectievakje niet is ingeschakeld, worden abonnementspogingen automatisch goedgekeurd.</span><span class="sxs-lookup"><span data-stu-id="a31d4-126">If the check box is not selected, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="a31d4-127">In dit voorbeeld worden abonnementen automatisch goedgekeurd, dus schakel het selectievakje niet in.</span><span class="sxs-lookup"><span data-stu-id="a31d4-127">In this example, subscriptions are automatically approved, so do not select the box.</span></span>

<span data-ttu-id="a31d4-128">Als u wilt toestaan dat ontwikkelaarsaccounts meerdere abonnementen op het nieuwe product hebben, schakelt u het selectievakje **Meerdere gelijktijdige abonnementen toestaan** in.</span><span class="sxs-lookup"><span data-stu-id="a31d4-128">To allow developer accounts to subscribe multiple times to the new product, select the **Allow multiple simultaneous subscriptions** check box.</span></span> <span data-ttu-id="a31d4-129">In deze zelfstudie worden meerdere gelijktijdige abonnementen niet gebruikt, dus laat het vakje uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a31d4-129">This tutorial does not utilize multiple simultaneous subscriptions, so leave it unchecked.</span></span>

<span data-ttu-id="a31d4-130">Nadat alle waarden zijn ingevoerd, klikt u op **Opslaan** om het product te maken.</span><span class="sxs-lookup"><span data-stu-id="a31d4-130">After all values are entered, click **Save** to create the product.</span></span>

![Product toegevoegd][api-management-product-added]

<span data-ttu-id="a31d4-132">Nieuwe producten zijn standaard zichtbaar voor gebruikers in de groep **Beheerders**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-132">By default, new products are visible to users in the **Administrators** group.</span></span> <span data-ttu-id="a31d4-133">We gaan de groep **Ontwikkelaars** toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a31d4-133">We are going to add the **Developers** group.</span></span> <span data-ttu-id="a31d4-134">Klik op **Gratis proefversie** en klik vervolgens op het tabblad **Zichtbaarheid**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-134">Click **Free Trial**, and then click the **Visibility** tab.</span></span>

> <span data-ttu-id="a31d4-135">In API Management worden groepen gebruikt voor het beheren van de zichtbaarheid van producten voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="a31d4-135">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="a31d4-136">Voor producten wordt zichtbaarheid aan groepen verleend en ontwikkelaars kunnen de producten bekijken en zich abonneren op de producten die zichtbaar zijn voor de groepen waartoe de ontwikkelaars behoren.</span><span class="sxs-lookup"><span data-stu-id="a31d4-136">Products grant visibility to groups, and developers can view and subscribe to the products that are visible to the groups in which they belong.</span></span> <span data-ttu-id="a31d4-137">Zie voor meer informatie [Groepen maken en gebruiken in Azure API Management][How to create and use groups in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="a31d4-137">For more information, see [How to create and use groups in Azure API Management][How to create and use groups in Azure API Management].</span></span>
> 
> 

![Ontwikkelaarsgroep toevoegen][api-management-add-developers-group]

<span data-ttu-id="a31d4-139">Schakel het selectievakje **Ontwikkelaars** in en klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-139">Select the **Developers** check box, and then click **Save**.</span></span>

## <span data-ttu-id="a31d4-140"><a name="add-api"> </a>Een API toevoegen aan het product</span><span class="sxs-lookup"><span data-stu-id="a31d4-140"><a name="add-api"> </a>To add an API to the product</span></span>
<span data-ttu-id="a31d4-141">In deze stap van de zelfstudie voegen we de Echo-API toe aan het nieuwe product Gratis proefversie.</span><span class="sxs-lookup"><span data-stu-id="a31d4-141">In this step of the tutorial, we will add the Echo API to the new Free Trial product.</span></span>

> <span data-ttu-id="a31d4-142">Elk service-exemplaar van API Management wordt al geconfigureerd geleverd met een Echo-API die kan worden gebruikt om te experimenteren met API Management en hier meer over te leren.</span><span class="sxs-lookup"><span data-stu-id="a31d4-142">Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="a31d4-143">Zie voor meer informatie [Uw eerste API beheren in Azure API Management][Manage your first API in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="a31d4-143">For more information, see [Manage your first API in Azure API Management][Manage your first API in Azure API Management].</span></span>
> 
> 

<span data-ttu-id="a31d4-144">Klik op **Producten** in het menu **API Management** aan de linkerkant en klik vervolgens op **Gratis proefversie** om het product te configureren.</span><span class="sxs-lookup"><span data-stu-id="a31d4-144">Click **Products** from the **API Management** menu on the left, and then click **Free Trial** to configure the product.</span></span>

![Product configureren][api-management-configure-product]

<span data-ttu-id="a31d4-146">Klik op **API toevoegen aan product**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-146">Click **Add API to product**.</span></span>

![API toevoegen aan product][api-management-add-api]

<span data-ttu-id="a31d4-148">Selecteer **Echo-API** en klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-148">Select **Echo API**, and then click **Save**.</span></span>

![Echo-API toevoegen][api-management-add-echo-api]

## <span data-ttu-id="a31d4-150"><a name="policies"> </a>Aanroepfrequentielimiet- en quotumbeleidsregels configureren</span><span class="sxs-lookup"><span data-stu-id="a31d4-150"><a name="policies"> </a>To configure call rate limit and quota policies</span></span>
<span data-ttu-id="a31d4-151">Frequentielimieten en quota worden geconfigureerd in de beleidseditor.</span><span class="sxs-lookup"><span data-stu-id="a31d4-151">Rate limits and quotas are configured in the policy editor.</span></span> <span data-ttu-id="a31d4-152">De twee beleidsregels die we in deze zelfstudie toevoegen, zijn [Aanroepfrequentie per abonnement beperken](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) en [Gebruiksquotum per abonnement instellen](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota).</span><span class="sxs-lookup"><span data-stu-id="a31d4-152">The two policies we will be adding in this tutorial are the [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="a31d4-153">Dit beleid moeten worden toegepast op het productbereik.</span><span class="sxs-lookup"><span data-stu-id="a31d4-153">These policies must be applied at the product scope.</span></span>

<span data-ttu-id="a31d4-154">Klik op **Beleidsregels** in het menu **API Management** aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="a31d4-154">Click **Policies** under the **API Management** menu on the left.</span></span> <span data-ttu-id="a31d4-155">Klik in de lijst **Product** op **Gratis proefversie**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-155">In the **Product** list, click **Free Trial**.</span></span>

![Productbeleid][api-management-product-policy]

<span data-ttu-id="a31d4-157">Klik op **Beleid toevoegen** om de beleidssjabloon te importeren en begin met het maken van de frequentielimiet- en quotumbeleidsregels.</span><span class="sxs-lookup"><span data-stu-id="a31d4-157">Click **Add Policy** to import the policy template and begin creating the rate limit and quota policies.</span></span>

![Beleid toevoegen][api-management-add-policy]

<span data-ttu-id="a31d4-159">Frequentielimiet- en quotumbeleidsregels zijn inkomende beleidsregels, dus plaats de cursor in het inkomende element.</span><span class="sxs-lookup"><span data-stu-id="a31d4-159">Rate limit and quota policies are inbound policies, so position the cursor in the inbound element.</span></span>

![Beleidseditor][api-management-policy-editor-inbound]

<span data-ttu-id="a31d4-161">Blader door de lijst met beleidsregels en zoek de beleidsvermelding **Aanroepfrequentie per abonnement beperken**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-161">Scroll through the list of policies and locate the **Limit call rate per subscription** policy entry.</span></span>

![Beleidsinstructies][api-management-limit-policies]

<span data-ttu-id="a31d4-163">Nadat de cursor in het **inkomende** beleidselement is geplaatst, klikt u op de pijl naast **Aanroepfrequentie per abonnement beperken** om de bijbehorende beleidssjabloon in te voegen.</span><span class="sxs-lookup"><span data-stu-id="a31d4-163">After the cursor is positioned in the **inbound** policy element, click the arrow beside **Limit call rate per subscription** to insert its policy template.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

<span data-ttu-id="a31d4-164">Zoals u in het codefragment kunt zien, kunt u met het beleid limieten instellen voor de API's en bewerkingen van het product.</span><span class="sxs-lookup"><span data-stu-id="a31d4-164">As you can see from the snippet, the policy allows setting limits for the product's APIs and operations.</span></span> <span data-ttu-id="a31d4-165">In deze zelfstudie maken we geen gebruik van die mogelijkheid, dus verwijder de elementen **api** en **operation** uit het element **rate-limit**, zodat alleen het buitenste element **rate-limit** overblijft, zoals in het volgende voorbeeld wordt getoond.</span><span class="sxs-lookup"><span data-stu-id="a31d4-165">In this tutorial we will not use that capability, so delete the **api** and **operation** elements from the **rate-limit** element, such that only the outer **rate-limit** element remains, as shown in the following example.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

<span data-ttu-id="a31d4-166">In het product Gratis proefversie is de maximaal toegestane aanroepfrequentie 10 aanroepen per minuut, dus typ **10** als de waarde voor het kenmerk **calls** en **60** voor het kenmerk **renewal-period**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-166">In the Free Trial product, the maximum allowable call rate is 10 calls per minute, so type **10** as the value for the **calls** attribute, and **60** for the **renewal-period** attribute.</span></span>

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

<span data-ttu-id="a31d4-167">Als u het beleid **Gebruiksquotum per abonnement instellen** wilt configureren, plaatst u de cursor direct onder het zojuist toegevoegde element **rate-limit** binnen het element **inbound** en klikt u vervolgens op de pijl links van **Gebruiksquotum per abonnement instellen**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-167">To configure the **Set usage quota per subscription** policy, position your cursor immediately below the newly added **rate-limit** element within the **inbound** element, and then locate and click the arrow to the left of **Set usage quota per subscription**.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

<span data-ttu-id="a31d4-168">Net als het beleid **Gebruiksquotum per abonnement instellen** kunt u met het beleid **Gebruiksquotum per abonnement instellen** limieten instellen voor de API's en bewerkingen van het product.</span><span class="sxs-lookup"><span data-stu-id="a31d4-168">Similarly to the **Set usage quota per subscription** policy, **Set usage quota per subscription** policy allows setting caps for on the product's APIs and operations.</span></span> <span data-ttu-id="a31d4-169">In deze zelfstudie maken we geen gebruik van die mogelijkheid, dus verwijder de elementen **api** en **operation** uit het element **quota**, zoals in het volgende voorbeeld wordt getoond.</span><span class="sxs-lookup"><span data-stu-id="a31d4-169">In this tutorial we will not use that capability, so delete the **api** and **operation** elements from the **quota** element, as shown in the following example.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

<span data-ttu-id="a31d4-170">Quota kunnen zijn gebaseerd op het aantal aanroepen per interval, de bandbreedte of beide.</span><span class="sxs-lookup"><span data-stu-id="a31d4-170">Quotas can be based on the number of calls per interval, bandwidth, or both.</span></span> <span data-ttu-id="a31d4-171">In deze zelfstudie beperken we niet op basis van bandbreedte, dus verwijder het kenmerk **bandwidth**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-171">In this tutorial, we are not throttling based on bandwidth, so delete the **bandwidth** attribute.</span></span>

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

<span data-ttu-id="a31d4-172">In het product Gratis proefversie is het quotum 200 aanroepen per week.</span><span class="sxs-lookup"><span data-stu-id="a31d4-172">In the Free Trial product, the quota is 200 calls per week.</span></span> <span data-ttu-id="a31d4-173">Geef **200** op als de waarde voor het kenmerk **calls** en geef vervolgens **604800** op als de waarde voor het kenmerk **renewal-period**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-173">Specify **200** as the value for the **calls** attribute, and then specify **604800** as the value for the **renewal-period** attribute.</span></span>

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> <span data-ttu-id="a31d4-174">Beleidsintervallen worden in seconden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="a31d4-174">Policy intervals are specified in seconds.</span></span> <span data-ttu-id="a31d4-175">Als u het interval voor een week wilt berekenen, kunt u het aantal dagen (7) vermenigvuldigen met het aantal uren in een dag (24) maal het aantal minuten in een uur (60) maal het aantal seconden in een minuut (60): 7 * 24 * 60 * 60 = 604800.</span><span class="sxs-lookup"><span data-stu-id="a31d4-175">To calculate the interval for a week, you can multiply the number of days (7) by the number of hours in a day (24) by the number of minutes in an hour (60) by the number of seconds in a minute (60): 7 * 24 * 60 * 60 = 604800.</span></span>
> 
> 

<span data-ttu-id="a31d4-176">Wanneer u klaar bent met het configureren van het beleid, moet het overeenkomen met het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="a31d4-176">When you have finished configuring the policy, it should match the following example.</span></span>

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

<span data-ttu-id="a31d4-177">Nadat de gewenste beleidsregels zijn geconfigureerd, klikt u op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-177">After the desired policies are configured, click **Save**.</span></span>

![Beleid opslaan][api-management-policy-save]

## <span data-ttu-id="a31d4-179"><a name="publish-product"> </a>Het product publiceren</span><span class="sxs-lookup"><span data-stu-id="a31d4-179"><a name="publish-product"> </a> To publish the product</span></span>
<span data-ttu-id="a31d4-180">Nu de API's zijn toegevoegd en de beleidsregels zijn geconfigureerd, moet het product worden gepubliceerd zodat het door ontwikkelaars kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a31d4-180">Now that the the APIs are added and the policies are configured, the product must be published so that it can be used by developers.</span></span> <span data-ttu-id="a31d4-181">Klik op **Producten** in het menu **API Management** aan de linkerkant en klik vervolgens op **Gratis proefversie** om het product te configureren.</span><span class="sxs-lookup"><span data-stu-id="a31d4-181">Click **Products** from the **API Management** menu on the left, and then click **Free Trial** to configure the product.</span></span>

![Product configureren][api-management-configure-product]

<span data-ttu-id="a31d4-183">Klik op **Publiceren** en klik vervolgens op **Ja, publiceren** om te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="a31d4-183">Click **Publish**, and then click **Yes, publish it** to confirm.</span></span>

![Product publiceren][api-management-publish-product]

## <span data-ttu-id="a31d4-185"><a name="subscribe-account"> </a>Een ontwikkelaarsaccount abonneren op het product</span><span class="sxs-lookup"><span data-stu-id="a31d4-185"><a name="subscribe-account"> </a>To subscribe a developer account to the product</span></span>
<span data-ttu-id="a31d4-186">Nu het product is gepubliceerd, is het beschikbaar voor ontwikkelaars om zich op te abonneren en om te worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a31d4-186">Now that the product is published, it is available to be subscribed to and used by developers.</span></span>

> <span data-ttu-id="a31d4-187">Beheerders van een API Management-exemplaar worden automatisch op elk product geabonneerd.</span><span class="sxs-lookup"><span data-stu-id="a31d4-187">Administrators of an API Management instance are automatically subscribed to every product.</span></span> <span data-ttu-id="a31d4-188">In deze zelfstudiestap abonneren we een van de ontwikkelaarsaccounts dat geen beheerdersaccount is op het product Gratis proefversie.</span><span class="sxs-lookup"><span data-stu-id="a31d4-188">In this tutorial step, we will subscribe one of the non-administrator developer accounts to the Free Trial product.</span></span> <span data-ttu-id="a31d4-189">Als uw ontwikkelaarsaccount deel uitmaakt van de rol Beheerder, kunt u doorgaan met deze stap, ook al bent u al geabonneerd.</span><span class="sxs-lookup"><span data-stu-id="a31d4-189">If your developer account is part of the Administrators role, then you can follow along with this step, even though you are already subscribed.</span></span>
> 
> 

<span data-ttu-id="a31d4-190">Klik op **Gebruikers** in het menu **API Management** aan de linkerkant en klik vervolgens op de naam van uw ontwikkelaarsaccount.</span><span class="sxs-lookup"><span data-stu-id="a31d4-190">Click **Users** on the **API Management** menu on the left, and then click the name of your developer account.</span></span> <span data-ttu-id="a31d4-191">In dit voorbeeld gebruiken we het ontwikkelaarsaccount **Floris Kregel**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-191">In this example, we are using the **Clayton Gragg** developer account.</span></span>

![Ontwikkelaar configureren][api-management-configure-developer]

<span data-ttu-id="a31d4-193">Klik op **Abonnement toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-193">Click **Add Subscription**.</span></span>

![Abonnement toevoegen][api-management-add-subscription-menu]

<span data-ttu-id="a31d4-195">Selecteer **Gratis proefversie** en klik vervolgens op **Abonneren**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-195">Select **Free Trial**, and then click **Subscribe**.</span></span>

![Abonnement toevoegen][api-management-add-subscription]

> [!NOTE]
> <span data-ttu-id="a31d4-197">In deze zelfstudie zijn meerdere gelijktijdige abonnementen niet ingeschakeld voor het product Gratis proefversie.</span><span class="sxs-lookup"><span data-stu-id="a31d4-197">In this tutorial, multiple simultaneous subscriptions are not enabled for the Free Trial product.</span></span> <span data-ttu-id="a31d4-198">Als dat wel het geval zou zijn, zou u om de naam van het abonnement worden gevraagd, zoals in het volgende voorbeeld wordt getoond.</span><span class="sxs-lookup"><span data-stu-id="a31d4-198">If they were, you would be prompted to name the subscription, as shown in the following example.</span></span>
> 
> 

![Abonnement toevoegen][api-management-add-subscription-multiple]

<span data-ttu-id="a31d4-200">Nadat u op **Abonneren** hebt geklikt, wordt het product weergegeven in de lijst **Abonnement** voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a31d4-200">After clicking **Subscribe**, the product appears in the **Subscription** list for the user.</span></span>

![Abonnement toegevoegd][api-management-subscription-added]

## <span data-ttu-id="a31d4-202"><a name="test-rate-limit"> </a>Een bewerking aanroepen en de frequentielimiet testen</span><span class="sxs-lookup"><span data-stu-id="a31d4-202"><a name="test-rate-limit"> </a>To call an operation and test the rate limit</span></span>
<span data-ttu-id="a31d4-203">Nu het product Gratis proefversie is geconfigureerd en gepubliceerd, kunnen we enkele bewerkingen aanroepen en het beleid voor frequentielimiet testen.</span><span class="sxs-lookup"><span data-stu-id="a31d4-203">Now that the Free Trial product is configured and published, we can call some operations and test the rate limit policy.</span></span>
<span data-ttu-id="a31d4-204">Schakel over naar de ontwikkelaarsportal door te klikken op **Ontwikkelaarsportal** in het menu rechtsboven.</span><span class="sxs-lookup"><span data-stu-id="a31d4-204">Switch to the developer portal by clicking **Developer portal** in the upper-right menu.</span></span>

![ontwikkelaarsportal][api-management-developer-portal-menu]

<span data-ttu-id="a31d4-206">Klik op **API's** in het bovenste menu en klik op **Echo-API**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-206">Click **APIs** in the top menu, and then click **Echo API**.</span></span>

![ontwikkelaarsportal][api-management-developer-portal-api-menu]

<span data-ttu-id="a31d4-208">Klik op **GET Resource** en klik vervolgens op **Probeer het nu**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-208">Click **GET Resource**, and then click **Try it**.</span></span>

![Console openen][api-management-open-console]

<span data-ttu-id="a31d4-210">Behoud de standaardparameterwaarden en selecteer uw abonnementssleutel voor het product Gratis proefversie.</span><span class="sxs-lookup"><span data-stu-id="a31d4-210">Keep the default parameter values, and then select your subscription key for the Free Trial product.</span></span>

![Abonnementssleutel][api-management-select-key]

> [!NOTE]
> <span data-ttu-id="a31d4-212">Als u meerdere abonnementen hebt, moet u ervoor zorgen dat u de sleutel voor **Gratis proefversie** selecteert, anders zijn de beleidsregels die in de vorige stappen zijn geconfigureerd niet van kracht.</span><span class="sxs-lookup"><span data-stu-id="a31d4-212">If you have multiple subscriptions, be sure to select the key for **Free Trial**, or else the policies that were configured in the previous steps won't be in effect.</span></span>
> 
> 

<span data-ttu-id="a31d4-213">Klik op **Verzenden** en bekijk vervolgens het antwoord.</span><span class="sxs-lookup"><span data-stu-id="a31d4-213">Click **Send**, and then view the response.</span></span> <span data-ttu-id="a31d4-214">Noteer de **Antwoordstatus** van **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="a31d4-214">Note the **Response status** of **200 OK**.</span></span>

![Bewerkingsresultaten][api-management-http-get-results]

<span data-ttu-id="a31d4-216">Klik op **Verzenden** met een hogere frequentie dan het beleid voor een frequentielimiet van 10 aanroepen per minuut.</span><span class="sxs-lookup"><span data-stu-id="a31d4-216">Click **Send** at a rate greater than the rate limit policy of 10 calls per minute.</span></span> <span data-ttu-id="a31d4-217">Nadat het beleid voor de frequentielimiet is overschreden, wordt een antwoordstatus van **429 te veel aanvragen** geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="a31d4-217">After the rate limit policy is exceeded, a response status of **429 Too Many Requests** is returned.</span></span>

![Bewerkingsresultaten][api-management-http-get-429]

<span data-ttu-id="a31d4-219">Met de **Antwoordinhoud** wordt het resterende interval aangegeven voordat nieuwe pogingen lukken.</span><span class="sxs-lookup"><span data-stu-id="a31d4-219">The **Response content** indicates the remaining interval before retries will be successful.</span></span>

<span data-ttu-id="a31d4-220">Wanneer het beleid voor een frequentielimiet van 10 aanroepen per minuut van kracht is, mislukken volgende aanroepen tot 60 seconden na de eerste van de 10 geslaagde aanroepen naar het product zijn verstreken voordat de frequentielimiet werd overschreden.</span><span class="sxs-lookup"><span data-stu-id="a31d4-220">When the rate limit policy of 10 calls per minute is in effect, subsequent calls will fail until 60 seconds have elapsed from the first of the 10 successful calls to the product before the rate limit was exceeded.</span></span> <span data-ttu-id="a31d4-221">In dit voorbeeld is het resterende interval 54 seconden.</span><span class="sxs-lookup"><span data-stu-id="a31d4-221">In this example, the remaining interval is 54 seconds.</span></span>

## <span data-ttu-id="a31d4-222"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a31d4-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="a31d4-223">Bekijk een demo voor het instellen van frequentielimieten en quota in de volgende video.</span><span class="sxs-lookup"><span data-stu-id="a31d4-223">Watch a demo of setting rate limits and quotas in the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How to create and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers to a product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API to the product]: #add-api
[Publish the product]: #publish-product
[Subscribe a developer account to the product]: #subscribe-account
[Call an operation and test the rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
