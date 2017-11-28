---
title: aaaProtect uw API met Azure API Management | Microsoft Docs
description: Meer informatie over hoe tooprotect uw API met quota's en beleidsregels (snelheidsbeperking) beperking.
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
ms.openlocfilehash: 3113fd277d434da0c051b8b90fd629a102bf4867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a><span data-ttu-id="a2917-103">Uw API beveiligen met frequentielimieten met behulp van Azure API Management</span><span class="sxs-lookup"><span data-stu-id="a2917-103">Protect your API with rate limits using Azure API Management</span></span>
<span data-ttu-id="a2917-104">Deze handleiding wordt getoond hoe eenvoudig het is tooadd beveiliging voor uw back-end API door aanroepfrequentielimiet-en quota configureren met Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="a2917-104">This guide shows you how easy it is tooadd protection for your backend API by configuring rate limit and quota policies with Azure API Management.</span></span>

<span data-ttu-id="a2917-105">In deze zelfstudie maakt u een ' API-product gratis proefversie waarmee ontwikkelaars toomake too10 aanroepen per minuut en up tooa maximaal 200 oproepen per week tooyour API met behulp van Hallo [aanroepfrequentie per abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) en [ Gebruiksquotum per abonnement instellen](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) beleid.</span><span class="sxs-lookup"><span data-stu-id="a2917-105">In this tutorial, you will create a "Free Trial" API product that allows developers toomake up too10 calls per minute and up tooa maximum of 200 calls per week tooyour API using hello [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="a2917-106">U wordt vervolgens Hallo API publiceren en Hallo het beleid voor frequentielimiet testen.</span><span class="sxs-lookup"><span data-stu-id="a2917-106">You will then publish hello API and test hello rate limit policy.</span></span>

<span data-ttu-id="a2917-107">Voor meer geavanceerde beperkingsscenario's met behulp van Hallo [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) en [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) beleid, Zie [geavanceerde aanvraagbeperking met Azure API Management](api-management-sample-flexible-throttling.md).</span><span class="sxs-lookup"><span data-stu-id="a2917-107">For more advanced throttling scenarios using hello [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies, see [Advanced request throttling with Azure API Management](api-management-sample-flexible-throttling.md).</span></span>

## <span data-ttu-id="a2917-108"><a name="create-product"></a>toocreate een product</span><span class="sxs-lookup"><span data-stu-id="a2917-108"><a name="create-product"> </a>toocreate a product</span></span>
<span data-ttu-id="a2917-109">In deze stap maakt u een product Gratis proefversie waarvoor geen abonnementsgoedkeuring is vereist.</span><span class="sxs-lookup"><span data-stu-id="a2917-109">In this step, you will create a Free Trial product that does not require subscription approval.</span></span>

> [!NOTE]
> <span data-ttu-id="a2917-110">Als u al een product geconfigureerd hebt en toouse wilt deze voor deze zelfstudie kunt u verdergaan te[configureren aanroepen snelheid en quotumbeleidsregels] [ Configure call rate limit and quota policies] en Hallo zelfstudie vanaf daar volgen met uw product in plaats van Hallo-product gratis proefversie.</span><span class="sxs-lookup"><span data-stu-id="a2917-110">If you already have a product configured and want toouse it for this tutorial, you can jump ahead too[Configure call rate limit and quota policies][Configure call rate limit and quota policies] and follow hello tutorial from there using your product in place of hello Free Trial product.</span></span>
> 
> 

<span data-ttu-id="a2917-111">tooget gestart, klikt u op **publicatieportal** in hello Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="a2917-111">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Publicatieportal][api-management-management-console]

> <span data-ttu-id="a2917-113">Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [uw eerste API beheren in Azure API Management] [ Manage your first API in Azure API Management] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a2917-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API in Azure API Management][Manage your first API in Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="a2917-114">Klik op **producten** in Hallo **API Management** menu op Hallo links toodisplay hello **producten** pagina.</span><span class="sxs-lookup"><span data-stu-id="a2917-114">Click **Products** in hello **API Management** menu on hello left toodisplay hello **Products** page.</span></span>

![Product toevoegen][api-management-add-product]

<span data-ttu-id="a2917-116">Klik op **product toevoegen** toodisplay hello **nieuw product toevoegen** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="a2917-116">Click **Add product** toodisplay hello **Add new product** dialog box.</span></span>

![Nieuw product toevoegen][api-management-new-product-window]

<span data-ttu-id="a2917-118">In Hallo **titel** in het vak **gratis proefversie**.</span><span class="sxs-lookup"><span data-stu-id="a2917-118">In hello **Title** box, type **Free Trial**.</span></span>

<span data-ttu-id="a2917-119">In Hallo **beschrijving** vak, type Hallo volgende tekst: **zijn abonnees kunnen toorun 10 aanroepen per minuut up tooa maximaal 200 aanroepen/week, waarna toegang wordt geweigerd.**</span><span class="sxs-lookup"><span data-stu-id="a2917-119">In hello **Description** box, type hello following text: **Subscribers will be able toorun 10 calls/minute up tooa maximum of 200 calls/week after which access is denied.**</span></span>

<span data-ttu-id="a2917-120">Producten in API Management kunnen worden beveiligd of open zijn.</span><span class="sxs-lookup"><span data-stu-id="a2917-120">Products in API Management can be protected or open.</span></span> <span data-ttu-id="a2917-121">Beveiligde producten moeten geabonneerde toobefore ze kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a2917-121">Protected products must be subscribed toobefore they can be used.</span></span> <span data-ttu-id="a2917-122">Open producten kunnen zonder abonnement worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a2917-122">Open products can be used without a subscription.</span></span> <span data-ttu-id="a2917-123">Zorg ervoor dat **abonnement vereisen** geselecteerde toocreate is een beveiligd product waarvoor een abonnement.</span><span class="sxs-lookup"><span data-stu-id="a2917-123">Ensure that **Require subscription** is selected toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="a2917-124">Dit is de standaardinstelling Hallo.</span><span class="sxs-lookup"><span data-stu-id="a2917-124">This is hello default setting.</span></span>

<span data-ttu-id="a2917-125">Als u wilt dat een beheerder tooreview en accepteren of weigeren abonnement toothis product probeert, selecteert u **goedkeuring abonnement vereisen**.</span><span class="sxs-lookup"><span data-stu-id="a2917-125">If you want an administrator tooreview and accept or reject subscription attempts toothis product, select **Require subscription approval**.</span></span> <span data-ttu-id="a2917-126">Als het selectievakje Hallo niet is ingeschakeld, worden abonnementspogingen automatisch goedgekeurd.</span><span class="sxs-lookup"><span data-stu-id="a2917-126">If hello check box is not selected, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="a2917-127">In dit voorbeeld worden abonnementen automatisch goedgekeurd, dus niet aanvinkt Hallo.</span><span class="sxs-lookup"><span data-stu-id="a2917-127">In this example, subscriptions are automatically approved, so do not select hello box.</span></span>

<span data-ttu-id="a2917-128">tooallow developer accounts toosubscribe meerdere keren toohello nieuw product, selecteer Hallo **meerdere gelijktijdige abonnementen toestaan** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="a2917-128">tooallow developer accounts toosubscribe multiple times toohello new product, select hello **Allow multiple simultaneous subscriptions** check box.</span></span> <span data-ttu-id="a2917-129">In deze zelfstudie worden meerdere gelijktijdige abonnementen niet gebruikt, dus laat het vakje uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a2917-129">This tutorial does not utilize multiple simultaneous subscriptions, so leave it unchecked.</span></span>

<span data-ttu-id="a2917-130">Nadat alle waarden zijn ingevoerd, klikt u op **opslaan** toocreate Hallo product.</span><span class="sxs-lookup"><span data-stu-id="a2917-130">After all values are entered, click **Save** toocreate hello product.</span></span>

![Product toegevoegd][api-management-product-added]

<span data-ttu-id="a2917-132">Nieuwe producten zijn standaard zichtbaar toousers in Hallo **beheerders** groep.</span><span class="sxs-lookup"><span data-stu-id="a2917-132">By default, new products are visible toousers in hello **Administrators** group.</span></span> <span data-ttu-id="a2917-133">We gaan tooadd hello **ontwikkelaars** groep.</span><span class="sxs-lookup"><span data-stu-id="a2917-133">We are going tooadd hello **Developers** group.</span></span> <span data-ttu-id="a2917-134">Klik op **gratis proefversie**, en klik vervolgens op Hallo **zichtbaarheid** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a2917-134">Click **Free Trial**, and then click hello **Visibility** tab.</span></span>

> <span data-ttu-id="a2917-135">Groepen zijn in API Management gebruikte toomanage Hallo zichtbaarheid van producten toodevelopers.</span><span class="sxs-lookup"><span data-stu-id="a2917-135">In API Management, groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="a2917-136">Voor producten wordt zichtbaarheid toogroups verleend en ontwikkelaars kunnen bekijken en zich abonneren toohello producten die zichtbaar toohello groepen waartoe ze behoren.</span><span class="sxs-lookup"><span data-stu-id="a2917-136">Products grant visibility toogroups, and developers can view and subscribe toohello products that are visible toohello groups in which they belong.</span></span> <span data-ttu-id="a2917-137">Zie voor meer informatie [hoe toocreate en gebruik groepen in Azure API Management][How toocreate and use groups in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="a2917-137">For more information, see [How toocreate and use groups in Azure API Management][How toocreate and use groups in Azure API Management].</span></span>
> 
> 

![Ontwikkelaarsgroep toevoegen][api-management-add-developers-group]

<span data-ttu-id="a2917-139">Selecteer Hallo **ontwikkelaars** selectievakje en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a2917-139">Select hello **Developers** check box, and then click **Save**.</span></span>

## <span data-ttu-id="a2917-140"><a name="add-api"></a>tooadd een API toohello product</span><span class="sxs-lookup"><span data-stu-id="a2917-140"><a name="add-api"> </a>tooadd an API toohello product</span></span>
<span data-ttu-id="a2917-141">In deze stap van de zelfstudie Hallo voegt Hallo Echo-API toohello nieuwe product gratis proefversie toe.</span><span class="sxs-lookup"><span data-stu-id="a2917-141">In this step of hello tutorial, we will add hello Echo API toohello new Free Trial product.</span></span>

> <span data-ttu-id="a2917-142">Elk exemplaar van API Management-service wordt geleverd met een Echo-API die kan worden gebruikt tooexperiment met en meer informatie over API Management vooraf geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="a2917-142">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="a2917-143">Zie voor meer informatie [Uw eerste API beheren in Azure API Management][Manage your first API in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="a2917-143">For more information, see [Manage your first API in Azure API Management][Manage your first API in Azure API Management].</span></span>
> 
> 

<span data-ttu-id="a2917-144">Klik op **producten** van Hallo **API Management** menu op Hallo links en klik vervolgens op **gratis proefversie** tooconfigure Hallo product.</span><span class="sxs-lookup"><span data-stu-id="a2917-144">Click **Products** from hello **API Management** menu on hello left, and then click **Free Trial** tooconfigure hello product.</span></span>

![Product configureren][api-management-configure-product]

<span data-ttu-id="a2917-146">Klik op **API toevoegen tooproduct**.</span><span class="sxs-lookup"><span data-stu-id="a2917-146">Click **Add API tooproduct**.</span></span>

![API-tooproduct toevoegen][api-management-add-api]

<span data-ttu-id="a2917-148">Selecteer **Echo-API** en klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a2917-148">Select **Echo API**, and then click **Save**.</span></span>

![Echo-API toevoegen][api-management-add-echo-api]

## <span data-ttu-id="a2917-150"><a name="policies"></a>tooconfigure aanroepen snelheid en quotumbeleidsregels</span><span class="sxs-lookup"><span data-stu-id="a2917-150"><a name="policies"> </a>tooconfigure call rate limit and quota policies</span></span>
<span data-ttu-id="a2917-151">Frequentielimieten en quota worden geconfigureerd in de beleidseditor Hallo.</span><span class="sxs-lookup"><span data-stu-id="a2917-151">Rate limits and quotas are configured in hello policy editor.</span></span> <span data-ttu-id="a2917-152">Hallo twee beleidsregels die we in deze zelfstudie gaat toevoegen zijn Hallo [aanroepfrequentie per abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) en [gebruiksquotum per abonnement instellen](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) beleid.</span><span class="sxs-lookup"><span data-stu-id="a2917-152">hello two policies we will be adding in this tutorial are hello [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="a2917-153">Dit beleid moeten worden toegepast op Hallo product bereik.</span><span class="sxs-lookup"><span data-stu-id="a2917-153">These policies must be applied at hello product scope.</span></span>

<span data-ttu-id="a2917-154">Klik op **beleid** onder Hallo **API Management** menu aan de linkerkant Hallo.</span><span class="sxs-lookup"><span data-stu-id="a2917-154">Click **Policies** under hello **API Management** menu on hello left.</span></span> <span data-ttu-id="a2917-155">In Hallo **Product** lijst, klikt u op **gratis proefversie**.</span><span class="sxs-lookup"><span data-stu-id="a2917-155">In hello **Product** list, click **Free Trial**.</span></span>

![Productbeleid][api-management-product-policy]

<span data-ttu-id="a2917-157">Klik op **beleid toevoegen** tooimport Hallo beleidssjabloon en begin met het maken van Hallo aanroepfrequentielimiet-en quotum.</span><span class="sxs-lookup"><span data-stu-id="a2917-157">Click **Add Policy** tooimport hello policy template and begin creating hello rate limit and quota policies.</span></span>

![Beleid toevoegen][api-management-add-policy]

<span data-ttu-id="a2917-159">Frequentie zijn en quotumbeleidsregels inkomende beleidsregels, geval positie Hallo cursor inkomende hello-element.</span><span class="sxs-lookup"><span data-stu-id="a2917-159">Rate limit and quota policies are inbound policies, so position hello cursor in hello inbound element.</span></span>

![Beleidseditor][api-management-policy-editor-inbound]

<span data-ttu-id="a2917-161">Schuif door Hallo lijst met beleidsregels en zoek Hallo **aanroepfrequentie per abonnement** beleidsvermelding.</span><span class="sxs-lookup"><span data-stu-id="a2917-161">Scroll through hello list of policies and locate hello **Limit call rate per subscription** policy entry.</span></span>

![Beleidsinstructies][api-management-limit-policies]

<span data-ttu-id="a2917-163">Na het Hallo cursor wordt geplaatst in Hallo **inkomende** beleidselement, klikt u op de pijl naast Hallo **aanroepfrequentie per abonnement** tooinsert bijbehorende beleidssjabloon.</span><span class="sxs-lookup"><span data-stu-id="a2917-163">After hello cursor is positioned in hello **inbound** policy element, click hello arrow beside **Limit call rate per subscription** tooinsert its policy template.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

<span data-ttu-id="a2917-164">Als u in het codefragment Hallo zien kunt, kunt Hallo beleid limieten instellen voor de API's en bewerkingen van het product Hallo.</span><span class="sxs-lookup"><span data-stu-id="a2917-164">As you can see from hello snippet, hello policy allows setting limits for hello product's APIs and operations.</span></span> <span data-ttu-id="a2917-165">In deze zelfstudie wordt er niet gebruiken die mogelijkheid, dus verwijder Hallo **api** en **bewerking** elementen uit Hallo **rate-limit** element, zodat alleen Hallo buitenste **rate-limit** overblijft, zoals weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="a2917-165">In this tutorial we will not use that capability, so delete hello **api** and **operation** elements from hello **rate-limit** element, such that only hello outer **rate-limit** element remains, as shown in hello following example.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

<span data-ttu-id="a2917-166">In het product gratis proefversie hello, Hallo maximaal toegestane aanroepfrequentie 10 aanroepen per minuut, dus typ **10** als waarde voor Hallo Hallo **aanroepen** kenmerk, en **60** voor Hallo **vernieuwingsperiode** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="a2917-166">In hello Free Trial product, hello maximum allowable call rate is 10 calls per minute, so type **10** as hello value for hello **calls** attribute, and **60** for hello **renewal-period** attribute.</span></span>

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

<span data-ttu-id="a2917-167">Hallo tooconfigure **gebruiksquotum per abonnement instellen** beleid, plaats de cursor direct onder Hallo toegevoegde **rate-limit** element in Hallo **binnenkomende** element en zoek vervolgens en klikt u op Hallo pijl toohello links van **gebruiksquotum per abonnement instellen**.</span><span class="sxs-lookup"><span data-stu-id="a2917-167">tooconfigure hello **Set usage quota per subscription** policy, position your cursor immediately below hello newly added **rate-limit** element within hello **inbound** element, and then locate and click hello arrow toohello left of **Set usage quota per subscription**.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

<span data-ttu-id="a2917-168">Op dezelfde manier toohello **gebruiksquotum per abonnement instellen** beleid, **gebruiksquotum per abonnement instellen** beleid kunt u de caps voor instelling op van het product Hallo API's en bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="a2917-168">Similarly toohello **Set usage quota per subscription** policy, **Set usage quota per subscription** policy allows setting caps for on hello product's APIs and operations.</span></span> <span data-ttu-id="a2917-169">In deze zelfstudie wordt er niet gebruiken die mogelijkheid, dus verwijder Hallo **api** en **bewerking** elementen uit Hallo **quotum** element, zoals wordt weergegeven in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="a2917-169">In this tutorial we will not use that capability, so delete hello **api** and **operation** elements from hello **quota** element, as shown in hello following example.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

<span data-ttu-id="a2917-170">Quota's kunnen worden gebaseerd op Hallo aantal aanroepen per interval, de bandbreedte of beide.</span><span class="sxs-lookup"><span data-stu-id="a2917-170">Quotas can be based on hello number of calls per interval, bandwidth, or both.</span></span> <span data-ttu-id="a2917-171">In deze zelfstudie beperken we niet op basis van bandbreedte, dus verwijder Hallo **bandbreedte** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="a2917-171">In this tutorial, we are not throttling based on bandwidth, so delete hello **bandwidth** attribute.</span></span>

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

<span data-ttu-id="a2917-172">Hallo-product gratis proefversie is Hallo quotum 200 oproepen per week.</span><span class="sxs-lookup"><span data-stu-id="a2917-172">In hello Free Trial product, hello quota is 200 calls per week.</span></span> <span data-ttu-id="a2917-173">Geef **200** als waarde voor Hallo Hallo **aanroepen** kenmerk en geef vervolgens **604800** als waarde voor Hallo Hallo **vernieuwingsperiode** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="a2917-173">Specify **200** as hello value for hello **calls** attribute, and then specify **604800** as hello value for hello **renewal-period** attribute.</span></span>

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> <span data-ttu-id="a2917-174">Beleidsintervallen worden in seconden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="a2917-174">Policy intervals are specified in seconds.</span></span> <span data-ttu-id="a2917-175">toocalculate hello-interval voor een week, kunt u het aantal dagen (7) door het aantal uren in een dag (24) door het aantal minuten in een uur (60) maal het aantal seconden in een minuut (60) Hallo Hallo HALLO hallo vermenigvuldigen: 7 * 24 * 60 * 60 = 604800.</span><span class="sxs-lookup"><span data-stu-id="a2917-175">toocalculate hello interval for a week, you can multiply hello number of days (7) by hello number of hours in a day (24) by hello number of minutes in an hour (60) by hello number of seconds in a minute (60): 7 * 24 * 60 * 60 = 604800.</span></span>
> 
> 

<span data-ttu-id="a2917-176">Wanneer u klaar bent met het Hallo-beleid configureren, moet het overeenkomen met Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="a2917-176">When you have finished configuring hello policy, it should match hello following example.</span></span>

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

<span data-ttu-id="a2917-177">Nadat het Hallo gewenste beleidsregels zijn geconfigureerd, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a2917-177">After hello desired policies are configured, click **Save**.</span></span>

![Beleid opslaan][api-management-policy-save]

## <span data-ttu-id="a2917-179"><a name="publish-product"></a> toopublish Hallo product</span><span class="sxs-lookup"><span data-stu-id="a2917-179"><a name="publish-product"> </a> toopublish hello product</span></span>
<span data-ttu-id="a2917-180">Nu dat hello hello API's toegevoegd en Hallo beleidsregels zijn geconfigureerd, moet Hallo product worden gepubliceerd zodat deze kan worden gebruikt door ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="a2917-180">Now that hello hello APIs are added and hello policies are configured, hello product must be published so that it can be used by developers.</span></span> <span data-ttu-id="a2917-181">Klik op **producten** van Hallo **API Management** menu op Hallo links en klik vervolgens op **gratis proefversie** tooconfigure Hallo product.</span><span class="sxs-lookup"><span data-stu-id="a2917-181">Click **Products** from hello **API Management** menu on hello left, and then click **Free Trial** tooconfigure hello product.</span></span>

![Product configureren][api-management-configure-product]

<span data-ttu-id="a2917-183">Klik op **publiceren**, en klik vervolgens op **Ja, publiceren** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="a2917-183">Click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span>

![Product publiceren][api-management-publish-product]

## <span data-ttu-id="a2917-185"><a name="subscribe-account"></a>toosubscribe een developer-account toohello product</span><span class="sxs-lookup"><span data-stu-id="a2917-185"><a name="subscribe-account"> </a>toosubscribe a developer account toohello product</span></span>
<span data-ttu-id="a2917-186">Nu dat Hallo-product is gepubliceerd, is beschikbaar toobe geabonneerd tooand gebruikt door ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="a2917-186">Now that hello product is published, it is available toobe subscribed tooand used by developers.</span></span>

> <span data-ttu-id="a2917-187">Beheerders van een exemplaar van API Management zijn automatisch geabonneerde tooevery product.</span><span class="sxs-lookup"><span data-stu-id="a2917-187">Administrators of an API Management instance are automatically subscribed tooevery product.</span></span> <span data-ttu-id="a2917-188">In deze zelfstudiestap abonneren we een Hallo beheerder developer accounts toohello-product gratis proefversie.</span><span class="sxs-lookup"><span data-stu-id="a2917-188">In this tutorial step, we will subscribe one of hello non-administrator developer accounts toohello Free Trial product.</span></span> <span data-ttu-id="a2917-189">Als uw ontwikkelaarsaccount deel van de rol Administrator hello uitmaakt, kunt klikt u vervolgens u met deze stap, zelfs als u bent al geabonneerd.</span><span class="sxs-lookup"><span data-stu-id="a2917-189">If your developer account is part of hello Administrators role, then you can follow along with this step, even though you are already subscribed.</span></span>
> 
> 

<span data-ttu-id="a2917-190">Klik op **gebruikers** op Hallo **API Management** menu op Hallo links en klik vervolgens op Hallo-naam van uw ontwikkelaarsaccount.</span><span class="sxs-lookup"><span data-stu-id="a2917-190">Click **Users** on hello **API Management** menu on hello left, and then click hello name of your developer account.</span></span> <span data-ttu-id="a2917-191">In dit voorbeeld gebruiken we Hallo **Clayton Gragg** developer-account.</span><span class="sxs-lookup"><span data-stu-id="a2917-191">In this example, we are using hello **Clayton Gragg** developer account.</span></span>

![Ontwikkelaar configureren][api-management-configure-developer]

<span data-ttu-id="a2917-193">Klik op **Abonnement toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a2917-193">Click **Add Subscription**.</span></span>

![Abonnement toevoegen][api-management-add-subscription-menu]

<span data-ttu-id="a2917-195">Selecteer **Gratis proefversie** en klik vervolgens op **Abonneren**.</span><span class="sxs-lookup"><span data-stu-id="a2917-195">Select **Free Trial**, and then click **Subscribe**.</span></span>

![Abonnement toevoegen][api-management-add-subscription]

> [!NOTE]
> <span data-ttu-id="a2917-197">In deze zelfstudie worden meerdere gelijktijdige abonnementen niet ingeschakeld voor Hallo-product gratis proefversie.</span><span class="sxs-lookup"><span data-stu-id="a2917-197">In this tutorial, multiple simultaneous subscriptions are not enabled for hello Free Trial product.</span></span> <span data-ttu-id="a2917-198">Als dat zo is, zou u na vragen aan gebruiker tooname Hallo abonnement, zoals weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="a2917-198">If they were, you would be prompted tooname hello subscription, as shown in hello following example.</span></span>
> 
> 

![Abonnement toevoegen][api-management-add-subscription-multiple]

<span data-ttu-id="a2917-200">Wanneer u op **abonneren**, Hallo product weergegeven in Hallo **abonnement** lijst voor Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a2917-200">After clicking **Subscribe**, hello product appears in hello **Subscription** list for hello user.</span></span>

![Abonnement toegevoegd][api-management-subscription-added]

## <span data-ttu-id="a2917-202"><a name="test-rate-limit"></a>toocall een bewerking en test Hallo frequentielimiet</span><span class="sxs-lookup"><span data-stu-id="a2917-202"><a name="test-rate-limit"> </a>toocall an operation and test hello rate limit</span></span>
<span data-ttu-id="a2917-203">Nu dat hello product gratis proefversie is geconfigureerd en gepubliceerd, kunnen we enkele bewerkingen aanroepen en Hallo het beleid voor frequentielimiet testen.</span><span class="sxs-lookup"><span data-stu-id="a2917-203">Now that hello Free Trial product is configured and published, we can call some operations and test hello rate limit policy.</span></span>
<span data-ttu-id="a2917-204">Switch toohello developer-portal door te klikken op **ontwikkelaarsportal** in het menu van Hallo rechtsboven.</span><span class="sxs-lookup"><span data-stu-id="a2917-204">Switch toohello developer portal by clicking **Developer portal** in hello upper-right menu.</span></span>

![ontwikkelaarsportal][api-management-developer-portal-menu]

<span data-ttu-id="a2917-206">Klik op **API's** in Hallo bovenste menu en klik vervolgens op **Echo-API**.</span><span class="sxs-lookup"><span data-stu-id="a2917-206">Click **APIs** in hello top menu, and then click **Echo API**.</span></span>

![ontwikkelaarsportal][api-management-developer-portal-api-menu]

<span data-ttu-id="a2917-208">Klik op **GET Resource** en klik vervolgens op **Probeer het nu**.</span><span class="sxs-lookup"><span data-stu-id="a2917-208">Click **GET Resource**, and then click **Try it**.</span></span>

![Console openen][api-management-open-console]

<span data-ttu-id="a2917-210">Gebruik Hallo standaardwaarde parameterwaarden en selecteer uw abonnementssleutel voor Hallo-product gratis proefversie.</span><span class="sxs-lookup"><span data-stu-id="a2917-210">Keep hello default parameter values, and then select your subscription key for hello Free Trial product.</span></span>

![Abonnementssleutel][api-management-select-key]

> [!NOTE]
> <span data-ttu-id="a2917-212">Als u meerdere abonnementen hebt, worden ervoor tooselect Hallo-sleutel voor **gratis proefversie**, of anders Hallo-beleidsregels die zijn geconfigureerd in de vorige stappen Hallo niet meer van kracht.</span><span class="sxs-lookup"><span data-stu-id="a2917-212">If you have multiple subscriptions, be sure tooselect hello key for **Free Trial**, or else hello policies that were configured in hello previous steps won't be in effect.</span></span>
> 
> 

<span data-ttu-id="a2917-213">Klik op **verzenden**, en bekijk vervolgens Hallo antwoord.</span><span class="sxs-lookup"><span data-stu-id="a2917-213">Click **Send**, and then view hello response.</span></span> <span data-ttu-id="a2917-214">Opmerking Hallo **antwoordstatus** van **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="a2917-214">Note hello **Response status** of **200 OK**.</span></span>

![Bewerkingsresultaten][api-management-http-get-results]

<span data-ttu-id="a2917-216">Klik op **verzenden** met een hogere frequentie dan Hallo beleid voor frequentielimiet van 10 aanroepen per minuut.</span><span class="sxs-lookup"><span data-stu-id="a2917-216">Click **Send** at a rate greater than hello rate limit policy of 10 calls per minute.</span></span> <span data-ttu-id="a2917-217">Nadat het beleid voor frequentielimiet Hallo is overschreden, een antwoordstatus van **429 te veel aanvragen** wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="a2917-217">After hello rate limit policy is exceeded, a response status of **429 Too Many Requests** is returned.</span></span>

![Bewerkingsresultaten][api-management-http-get-429]

<span data-ttu-id="a2917-219">Hallo **antwoordinhoud** geeft Hallo resterende interval voordat nieuwe pogingen lukken.</span><span class="sxs-lookup"><span data-stu-id="a2917-219">hello **Response content** indicates hello remaining interval before retries will be successful.</span></span>

<span data-ttu-id="a2917-220">Wanneer beleid voor Hallo frequentielimiet van 10 aanroepen per minuut van kracht is, mislukken volgende aanroepen tot 60 seconden na Hallo eerste Hallo 10 geslaagde aanroepen toohello product voordat Hallo frequentielimiet werd overschreden.</span><span class="sxs-lookup"><span data-stu-id="a2917-220">When hello rate limit policy of 10 calls per minute is in effect, subsequent calls will fail until 60 seconds have elapsed from hello first of hello 10 successful calls toohello product before hello rate limit was exceeded.</span></span> <span data-ttu-id="a2917-221">In dit voorbeeld is Hallo resterende interval 54 seconden.</span><span class="sxs-lookup"><span data-stu-id="a2917-221">In this example, hello remaining interval is 54 seconds.</span></span>

## <span data-ttu-id="a2917-222"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a2917-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="a2917-223">Bekijk een demo voor het instellen van frequentielimieten en quota in Hallo video te volgen.</span><span class="sxs-lookup"><span data-stu-id="a2917-223">Watch a demo of setting rate limits and quotas in hello following video.</span></span>

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How toocreate and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers tooa product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API toohello product]: #add-api
[Publish hello product]: #publish-product
[Subscribe a developer account toohello product]: #subscribe-account
[Call an operation and test hello rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
