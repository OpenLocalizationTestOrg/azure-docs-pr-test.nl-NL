---
title: HTTP-instelling met de engine van Azure CDN regels wijzigen | Microsoft Docs
description: "De regelengine voor kunt u aanpassen hoe HTTP-aanvragen worden verwerkt door Azure CDN, zoals de levering van bepaalde typen inhoud blokkeren, een cachebeleid definiëren en aanpassen van HTTP-headers."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: abfe283476206b181018d187675b47112dc5ad2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="override-http-behavior-using-the-azure-cdn-rules-engine"></a><span data-ttu-id="ee0f7-103">HTTP-instelling met de engine van Azure CDN regels wijzigen</span><span class="sxs-lookup"><span data-stu-id="ee0f7-103">Override HTTP behavior using the Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="ee0f7-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="ee0f7-104">Overview</span></span>
<span data-ttu-id="ee0f7-105">De regelengine voor kunt u aanpassen hoe HTTP-aanvragen worden verwerkt, zoals de levering van bepaalde typen inhoud blokkeren, een cachebeleid definiëren en HTTP-headers wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-105">The rules engine allows you to customize how HTTP requests are handled, such as blocking the delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="ee0f7-106">Deze zelfstudie wordt gedemonstreerd maken van een regel waarmee het cachegedrag van CDN activa wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-106">This tutorial will demonstrate creating a rule that will change the caching behavior of CDN assets.</span></span>  <span data-ttu-id="ee0f7-107">Er is ook video-inhoud beschikbaar in de '[Zie ook](#see-also)' sectie.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-107">There's also video content available in the "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="ee0f7-108">Zie voor een verwijzing naar de syntaxis in detail, [regels Engine verwijzing](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="ee0f7-108">For a reference to the syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="ee0f7-109">Zelfstudie</span><span class="sxs-lookup"><span data-stu-id="ee0f7-109">Tutorial</span></span>
1. <span data-ttu-id="ee0f7-110">Klik in de blade CDN-profiel op de **beheren** knop.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-110">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Knop blade CDN-profiel beheren](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="ee0f7-112">Hiermee opent u de CDN-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-112">The CDN management portal opens.</span></span>
2. <span data-ttu-id="ee0f7-113">Klik op de **HTTP grote** tabblad, gevolgd door **regelengine**.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-113">Click on the **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="ee0f7-114">Opties voor een nieuwe regel worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-114">Options for a new rule are displayed.</span></span>
   
    ![Opties voor nieuwe CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="ee0f7-116">De volgorde waarin u meerdere regels staan is van invloed op hoe ze worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-116">The order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="ee0f7-117">Een volgende regel mogen de handelingen die zijn opgegeven door een vorige regel overschrijven.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-117">A subsequent rule may override the actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="ee0f7-118">Voer een naam in de **naam / beschrijving** textbox.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-118">Enter a name in the **Name / Description** textbox.</span></span>
4. <span data-ttu-id="ee0f7-119">Identificeer het type van de regel wordt toegepast op aanvragen.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-119">Identify the type of requests the rule will apply to.</span></span>  <span data-ttu-id="ee0f7-120">Standaard de **altijd** overeen voorwaarde is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-120">By default, the **Always** match condition is selected.</span></span>  <span data-ttu-id="ee0f7-121">U **altijd** voor deze zelfstudie, dus laat die geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![CDN overeen voorwaarde](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="ee0f7-123">Er zijn veel soorten overeenkomst voorwaarden die beschikbaar zijn in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-123">There are many types of match conditions available in the dropdown.</span></span>  <span data-ttu-id="ee0f7-124">Op de blauwe informatief pictogram aan de linkerkant van de conditie van de overeenkomst te klikken, wordt de geselecteerde voorwaarde in detail uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-124">Clicking on the blue informational icon to the left of the match condition will explain the currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="ee0f7-125">Zie voor een volledige lijst met voorwaardelijke expressies in detail, [regels Engine voorwaardelijke expressies](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="ee0f7-125">For the full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="ee0f7-126">Zie voor een volledige lijst met voorwaarden in detail overeen, [regels overeenkomen met motor](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="ee0f7-126">For the full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="ee0f7-127">Klik op de  **+**  naast **functies** een nieuwe functie toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-127">Click the **+** button next to **Features** to add a new feature.</span></span>  <span data-ttu-id="ee0f7-128">Selecteer in de vervolgkeuzelijst aan de linkerkant **Force interne-maximumleeftijd**.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-128">In the dropdown on the left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="ee0f7-129">Voer in het tekstvak dat wordt weergegeven, **300**.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-129">In the textbox that appears, enter **300**.</span></span>  <span data-ttu-id="ee0f7-130">Laat de overige standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-130">Leave the remaining default values.</span></span>
   
   ![CDN-functie](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="ee0f7-132">Als met de voorwaarden van de overeenkomst geeft te klikken op de blauwe informatief pictogram aan de linkerkant van de nieuwe functie informatie over deze functie.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-132">As with match conditions, clicking the blue informational icon to the left of the new feature will display details about this feature.</span></span>  <span data-ttu-id="ee0f7-133">In het geval van **Force interne-maximumleeftijd**, wordt bij het overschrijven van de asset **Cache-Control** en **verloopt** headers om te bepalen wanneer de activa van wordt vernieuwd in het CDN edge-knooppunt de oorsprong.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-133">In the case of **Force Internal Max-Age**, we are overriding the asset's **Cache-Control** and **Expires** headers to control when the CDN edge node will refresh the asset from the origin.</span></span>  <span data-ttu-id="ee0f7-134">Het voorbeeld van 300 seconden betekent dat het edge-knooppunt van het CDN cache worden opgeslagen door de asset gedurende vijf minuten voordat u de asset van de oorspronkelijke vernieuwt.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-134">Our example of 300 seconds means the CDN edge node will cache the asset for 5 minutes before refreshing the asset from its origin.</span></span>
   > 
   > <span data-ttu-id="ee0f7-135">Zie voor een volledige lijst met functies in detail [regels Engine functie Details](cdn-rules-engine-reference-features.md).</span><span class="sxs-lookup"><span data-stu-id="ee0f7-135">For the full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="ee0f7-136">Klik op de **toevoegen** om op te slaan van de nieuwe regel.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-136">Click the **Add** button to save the new rule.</span></span>  <span data-ttu-id="ee0f7-137">De nieuwe regel wordt nu in afwachting van goedkeuring.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-137">The new rule is now awaiting approval.</span></span> <span data-ttu-id="ee0f7-138">Zodra deze is goedgekeurd, de status verandert van **in behandeling XML** naar **Active XML**.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-138">Once it has been approved, the status will change from **Pending XML** to **Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="ee0f7-139">Regels wijzigingen kunnen worden doorgegeven via de CDN tot 90 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="ee0f7-139">Rules changes may take up to 90 minutes to propagate through the CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="ee0f7-140">Zie ook</span><span class="sxs-lookup"><span data-stu-id="ee0f7-140">See also</span></span>
* [<span data-ttu-id="ee0f7-141">Overzicht van Azure CDN</span><span class="sxs-lookup"><span data-stu-id="ee0f7-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="ee0f7-142">Regels Engine verwijzing</span><span class="sxs-lookup"><span data-stu-id="ee0f7-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="ee0f7-143">De overeenkomst motor regels</span><span class="sxs-lookup"><span data-stu-id="ee0f7-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="ee0f7-144">Regels Engine voorwaardelijke expressies</span><span class="sxs-lookup"><span data-stu-id="ee0f7-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="ee0f7-145">Regels Engine functies</span><span class="sxs-lookup"><span data-stu-id="ee0f7-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="ee0f7-146">Standaardgedrag HTTP met de regelengine van</span><span class="sxs-lookup"><span data-stu-id="ee0f7-146">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="ee0f7-147">[Azure vrijdag: Azure CDN krachtige nieuwe Premiumfuncties](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span><span class="sxs-lookup"><span data-stu-id="ee0f7-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>