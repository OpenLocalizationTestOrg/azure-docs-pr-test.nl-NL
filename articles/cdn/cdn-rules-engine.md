---
title: aaaOverride HTTP gedrag met hello Azure CDN regelengine | Microsoft Docs
description: "Hallo regels-engine kunt u toocustomize hoe HTTP-aanvragen worden verwerkt door Azure CDN, zoals een blokkade Hallo levering van bepaalde typen inhoud, een cachebeleid definiëren en HTTP-headers wijzigen."
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
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a><span data-ttu-id="47d35-103">HTTP-gedrag met hello Azure CDN regelengine overschrijven</span><span class="sxs-lookup"><span data-stu-id="47d35-103">Override HTTP behavior using hello Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="47d35-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="47d35-104">Overview</span></span>
<span data-ttu-id="47d35-105">Hallo-engine voor regels kunt u toocustomize hoe HTTP-aanvragen worden verwerkt, zoals Hallo levering van bepaalde typen inhoud blokkeren, een cachebeleid definiëren en HTTP-headers wijzigen.</span><span class="sxs-lookup"><span data-stu-id="47d35-105">hello rules engine allows you toocustomize how HTTP requests are handled, such as blocking hello delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="47d35-106">Deze zelfstudie wordt gedemonstreerd Hallo cachegedrag van CDN activa maken van een regel die wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="47d35-106">This tutorial will demonstrate creating a rule that will change hello caching behavior of CDN assets.</span></span>  <span data-ttu-id="47d35-107">Er is ook video-inhoud beschikbaar in Hallo '[Zie ook](#see-also)' sectie.</span><span class="sxs-lookup"><span data-stu-id="47d35-107">There's also video content available in hello "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="47d35-108">Zie voor een syntaxis van de toohello verwijzing in detail [regels Engine verwijzing](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="47d35-108">For a reference toohello syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="47d35-109">Zelfstudie</span><span class="sxs-lookup"><span data-stu-id="47d35-109">Tutorial</span></span>
1. <span data-ttu-id="47d35-110">Blade voor Hallo CDN-profiel, klik op Hallo **beheren** knop.</span><span class="sxs-lookup"><span data-stu-id="47d35-110">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Knop blade CDN-profiel beheren](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="47d35-112">Hallo CDN-beheerportal geopend.</span><span class="sxs-lookup"><span data-stu-id="47d35-112">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="47d35-113">Klik op Hallo **HTTP grote** tabblad, gevolgd door **regelengine**.</span><span class="sxs-lookup"><span data-stu-id="47d35-113">Click on hello **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="47d35-114">Opties voor een nieuwe regel worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="47d35-114">Options for a new rule are displayed.</span></span>
   
    ![Opties voor nieuwe CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="47d35-116">Hallo volgorde meerdere regels zijn van invloed op hoe ze worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="47d35-116">hello order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="47d35-117">Een volgende regel mogen Hallo handelingen die zijn opgegeven door een vorige regel overschrijven.</span><span class="sxs-lookup"><span data-stu-id="47d35-117">A subsequent rule may override hello actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="47d35-118">Voer een naam in Hallo **naam / beschrijving** textbox.</span><span class="sxs-lookup"><span data-stu-id="47d35-118">Enter a name in hello **Name / Description** textbox.</span></span>
4. <span data-ttu-id="47d35-119">Identificeer Hallo type aanvragen Hallo regel van toepassing.</span><span class="sxs-lookup"><span data-stu-id="47d35-119">Identify hello type of requests hello rule will apply to.</span></span>  <span data-ttu-id="47d35-120">Standaard Hallo **altijd** overeen voorwaarde is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="47d35-120">By default, hello **Always** match condition is selected.</span></span>  <span data-ttu-id="47d35-121">U **altijd** voor deze zelfstudie, dus laat die geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="47d35-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![CDN overeen voorwaarde](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="47d35-123">Er zijn veel soorten overeen beschikbaar in de vervolgkeuzelijst Hallo voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="47d35-123">There are many types of match conditions available in hello dropdown.</span></span>  <span data-ttu-id="47d35-124">Te klikken op Hallo blauw pictogram informatief toohello wordt links van Hallo overeen voorwaarde Hallo geselecteerde voorwaarde in detail uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="47d35-124">Clicking on hello blue informational icon toohello left of hello match condition will explain hello currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="47d35-125">Zie voor volledige lijst van voorwaardelijke expressies in detail Hallo [regels Engine voorwaardelijke expressies](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="47d35-125">For hello full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="47d35-126">Zie voor volledige lijst van voorwaarden van de overeenkomst in detail Hallo [regels overeenkomen met motor](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="47d35-126">For hello full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="47d35-127">Klik op Hallo  **+**  knop naast te**functies** tooadd een nieuwe functie.</span><span class="sxs-lookup"><span data-stu-id="47d35-127">Click hello **+** button next too**Features** tooadd a new feature.</span></span>  <span data-ttu-id="47d35-128">Selecteer in de vervolgkeuzelijst aan de linkerkant Hallo Hallo **Force interne-maximumleeftijd**.</span><span class="sxs-lookup"><span data-stu-id="47d35-128">In hello dropdown on hello left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="47d35-129">Voer in het tekstvak Hallo die wordt weergegeven, **300**.</span><span class="sxs-lookup"><span data-stu-id="47d35-129">In hello textbox that appears, enter **300**.</span></span>  <span data-ttu-id="47d35-130">Laat Hallo resterende standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="47d35-130">Leave hello remaining default values.</span></span>
   
   ![CDN-functie](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="47d35-132">Omdat met de voorwaarden van de overeenkomst, te klikken op Hallo blauw pictogram informatief toohello Hallo nieuwe weergegeven functie details over deze functie.</span><span class="sxs-lookup"><span data-stu-id="47d35-132">As with match conditions, clicking hello blue informational icon toohello left of hello new feature will display details about this feature.</span></span>  <span data-ttu-id="47d35-133">In geval van Hallo **Force interne-maximumleeftijd**, zijn we van Hallo actief overschrijven **Cache-Control** en **verloopt** headers toocontrol wanneer Hallo CDN edge-knooppunt wordt Hallo vernieuwen Asset vanuit Hallo oorsprong.</span><span class="sxs-lookup"><span data-stu-id="47d35-133">In hello case of **Force Internal Max-Age**, we are overriding hello asset's **Cache-Control** and **Expires** headers toocontrol when hello CDN edge node will refresh hello asset from hello origin.</span></span>  <span data-ttu-id="47d35-134">Het voorbeeld van 300 seconden betekent Hallo CDN edge-knooppunt wordt in de cache Hallo asset vijf minuten vóór vernieuwen Hallo asset vanuit de oorsprong.</span><span class="sxs-lookup"><span data-stu-id="47d35-134">Our example of 300 seconds means hello CDN edge node will cache hello asset for 5 minutes before refreshing hello asset from its origin.</span></span>
   > 
   > <span data-ttu-id="47d35-135">Zie voor een volledige lijst met functies in detail Hallo [regels Engine functie Details](cdn-rules-engine-reference-features.md).</span><span class="sxs-lookup"><span data-stu-id="47d35-135">For hello full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="47d35-136">Klik op Hallo **toevoegen** knop toosave Hallo nieuwe regel.</span><span class="sxs-lookup"><span data-stu-id="47d35-136">Click hello **Add** button toosave hello new rule.</span></span>  <span data-ttu-id="47d35-137">de nieuwe regel Hallo nu wacht op goedkeuring.</span><span class="sxs-lookup"><span data-stu-id="47d35-137">hello new rule is now awaiting approval.</span></span> <span data-ttu-id="47d35-138">Zodra deze is goedgekeurd, Hallo status verandert van **in behandeling XML** te**Active XML**.</span><span class="sxs-lookup"><span data-stu-id="47d35-138">Once it has been approved, hello status will change from **Pending XML** too**Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="47d35-139">Up too90 minuten toopropagate via Hallo CDN kan duren voordat wijzigingen in regels.</span><span class="sxs-lookup"><span data-stu-id="47d35-139">Rules changes may take up too90 minutes toopropagate through hello CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="47d35-140">Zie ook</span><span class="sxs-lookup"><span data-stu-id="47d35-140">See also</span></span>
* [<span data-ttu-id="47d35-141">Overzicht van Azure CDN</span><span class="sxs-lookup"><span data-stu-id="47d35-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="47d35-142">Regels Engine verwijzing</span><span class="sxs-lookup"><span data-stu-id="47d35-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="47d35-143">De overeenkomst motor regels</span><span class="sxs-lookup"><span data-stu-id="47d35-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="47d35-144">Regels Engine voorwaardelijke expressies</span><span class="sxs-lookup"><span data-stu-id="47d35-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="47d35-145">Regels Engine functies</span><span class="sxs-lookup"><span data-stu-id="47d35-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="47d35-146">Standaardgedrag HTTP met Hallo regelengine</span><span class="sxs-lookup"><span data-stu-id="47d35-146">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="47d35-147">[Azure vrijdag: Azure CDN krachtige nieuwe Premiumfuncties](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span><span class="sxs-lookup"><span data-stu-id="47d35-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>