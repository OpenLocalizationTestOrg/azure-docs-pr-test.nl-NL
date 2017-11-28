---
title: aaaGetting de slag met Azure CDN | Microsoft Docs
description: Dit onderwerp leest hoe tooenable hello Azure Content Delivery Network (CDN). Hallo-zelfstudie wordt begeleid Hallo maken van een nieuw CDN-profiel en -eindpunt.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a><span data-ttu-id="f5271-104">Aan de slag met Azure CDN</span><span class="sxs-lookup"><span data-stu-id="f5271-104">Getting started with Azure CDN</span></span>
<span data-ttu-id="f5271-105">In dit onderwerp wordt uitgelegd hoe u Azure CDN inschakelt door een nieuw CDN-profiel en -eindpunt te maken.</span><span class="sxs-lookup"><span data-stu-id="f5271-105">This topic walks through enabling Azure CDN by creating a new CDN profile and endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f5271-106">Zie voor een inleiding toohow CDN werkt, evenals een lijst met functies, Hallo [overzicht van CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f5271-106">For an introduction toohow CDN works, as well as a list of features, see hello [CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="f5271-107">Nieuwe CDN-profielen maken</span><span class="sxs-lookup"><span data-stu-id="f5271-107">Create a new CDN profile</span></span>
<span data-ttu-id="f5271-108">Een CDN-profiel is een verzameling van CDN-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="f5271-108">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="f5271-109">Elk profiel bevat een of meer CDN-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="f5271-109">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="f5271-110">U kunt desgewenst toouse meerdere profielen tooorganize uw CDN-eindpunten door internetdomein, webtoepassing of andere criteria.</span><span class="sxs-lookup"><span data-stu-id="f5271-110">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="f5271-111">Eén Azure-abonnement is standaard beperkt tooeight CDN-profielen.</span><span class="sxs-lookup"><span data-stu-id="f5271-111">By default, a single Azure subscription is limited tooeight CDN profiles.</span></span> <span data-ttu-id="f5271-112">Elk CDN-profiel is beperkt tooten CDN-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="f5271-112">Each CDN profile is limited tooten CDN endpoints.</span></span>
> 
> <span data-ttu-id="f5271-113">Prijzen van CDN wordt toegepast op Hallo CDN-profiel niveau.</span><span class="sxs-lookup"><span data-stu-id="f5271-113">CDN pricing is applied at hello CDN profile level.</span></span> <span data-ttu-id="f5271-114">Als u toouse een combinatie van Azure CDN Prijscategorieën wenst, moet u meerdere CDN-profielen.</span><span class="sxs-lookup"><span data-stu-id="f5271-114">If you wish toouse a mix of Azure CDN pricing tiers, you will need multiple CDN profiles.</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="f5271-115">Nieuwe CDN-eindpunten maken</span><span class="sxs-lookup"><span data-stu-id="f5271-115">Create a new CDN endpoint</span></span>
<span data-ttu-id="f5271-116">**toocreate een nieuw CDN-eindpunt**</span><span class="sxs-lookup"><span data-stu-id="f5271-116">**toocreate a new CDN endpoint**</span></span>

1. <span data-ttu-id="f5271-117">In Hallo [Azure Portal](https://portal.azure.com), navigeer tooyour CDN-profiel.</span><span class="sxs-lookup"><span data-stu-id="f5271-117">In hello [Azure Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="f5271-118">U kunt hebt vastgemaakt toohello dashboard in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="f5271-118">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="f5271-119">Als u niet, u kunt vinden door te klikken op **Bladeren**, klikt u vervolgens **CDN-profielen**, en te klikken op Hallo profiel u van plan bent tooadd het eindpunt.</span><span class="sxs-lookup"><span data-stu-id="f5271-119">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="f5271-120">blade Hallo CDN-profiel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f5271-120">hello CDN profile blade appears.</span></span>
   
    ![CDN-profiel][cdn-profile-settings]
2. <span data-ttu-id="f5271-122">Klik op Hallo **eindpunt toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="f5271-122">Click hello **Add Endpoint** button.</span></span>
   
    ![De knop Eindpunt toevoegen][cdn-new-endpoint-button]
   
    <span data-ttu-id="f5271-124">Hallo **een eindpunt toevoegen** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f5271-124">hello **Add an endpoint** blade appears.</span></span>
   
    ![De blade Een eindpunt toevoegen][cdn-add-endpoint]
3. <span data-ttu-id="f5271-126">Voer een **naam** voor dit CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="f5271-126">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="f5271-127">Deze naam worden uw resources in de cache op Hallo domein gebruikte tooaccess `<endpointname>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="f5271-127">This name will be used tooaccess your cached resources at hello domain `<endpointname>.azureedge.net`.</span></span>
4. <span data-ttu-id="f5271-128">In Hallo **oorsprongtype** vervolgkeuzelijst selecteert u het oorsprongtype.</span><span class="sxs-lookup"><span data-stu-id="f5271-128">In hello **Origin type** dropdown, select your origin type.</span></span>  <span data-ttu-id="f5271-129">Selecteer **Storage** voor een Azure Storage-account, **Cloudservice** voor een Azure Cloud-service, **Web App** voor een Azure-webtoepassing of **Aangepaste oorsprong** voor een andere openbaar toegankelijke webserveroorsprong (gehost in Azure of ergens anders).</span><span class="sxs-lookup"><span data-stu-id="f5271-129">Select **Storage** for an Azure Storage account, **Cloud service** for an Azure Cloud Service, **Web App** for an Azure Web App, or **Custom origin** for any other publicly accessible web server origin (hosted in Azure or elsewhere).</span></span>
   
    ![Oorsprongtype CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. <span data-ttu-id="f5271-131">In Hallo **de hostnaam van oorsprong** vervolgkeuzelijst, selecteer of typ uw brondomein.</span><span class="sxs-lookup"><span data-stu-id="f5271-131">In hello **Origin hostname** dropdown, select or type your origin domain.</span></span>  <span data-ttu-id="f5271-132">Hallo vervolgkeuzelijst bevat alle beschikbare oorsprongen van het Hallo-type die u hebt opgegeven in stap 4.</span><span class="sxs-lookup"><span data-stu-id="f5271-132">hello dropdown will list all available origins of hello type you specified in step 4.</span></span>  <span data-ttu-id="f5271-133">Als u hebt geselecteerd *aangepaste oorsprong* als uw **oorsprongtype**, voert u Hallo domein van uw aangepaste oorsprong.</span><span class="sxs-lookup"><span data-stu-id="f5271-133">If you selected *Custom origin* as your **Origin type**, you will type in hello domain of your custom origin.</span></span>
6. <span data-ttu-id="f5271-134">In Hallo **oorsprongpad** tekst Voer Hallo pad toohello bronnen die u wilt toocache of laat de eigenschap leeg tooallow cache alle resource in Hallo domein dat u in stap 5 hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f5271-134">In hello **Origin path** text box, enter hello path toohello resources you want toocache, or leave blank tooallow cache any resource at hello domain you specified in step 5.</span></span>
7. <span data-ttu-id="f5271-135">In Hallo **host-header van oorsprong**, Voer Hallo host-header gewenste Hallo CDN toosend bij elke aanvraag of laat de standaardwaarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="f5271-135">In hello **Origin host header**, enter hello host header you want hello CDN toosend with each request, or leave hello default.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="f5271-136">Bepaalde oorsprongtypen, zoals Azure Storage en Web-Apps, vereisen Hallo host-header toomatch Hallo domein van de oorsprong Hallo.</span><span class="sxs-lookup"><span data-stu-id="f5271-136">Some types of origins, such as Azure Storage and Web Apps, require hello host header toomatch hello domain of hello origin.</span></span> <span data-ttu-id="f5271-137">Tenzij u een bron die een host-header verschilt van het domein vereist hebt, laat u Hallo-standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="f5271-137">Unless you have an origin that requires a host header different from its domain, you should leave hello default value.</span></span>
   > 
   > 
8. <span data-ttu-id="f5271-138">Voor **Protocol** en **poort van oorsprong**, geeft u Hallo-protocollen en poorten gebruikt tooaccess uw resources op Hallo oorsprong.</span><span class="sxs-lookup"><span data-stu-id="f5271-138">For **Protocol** and **Origin port**, specify hello protocols and ports used tooaccess your resources at hello origin.</span></span>  <span data-ttu-id="f5271-139">Er moet minimaal één protocol (HTTP of HTTPS) worden geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f5271-139">At least one protocol (HTTP or HTTPS) must be selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f5271-140">Hallo **poort van oorsprong** alleen van invloed op welke poort Hallo-eindpunt maakt gebruik van informatie van de oorsprong Hallo tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="f5271-140">hello **Origin port** only affects what port hello endpoint uses tooretrieve information from hello origin.</span></span>  <span data-ttu-id="f5271-141">Hallo eindpunt zelf worden pas beschikbaar tooend clients op Hallo standaard HTTP en HTTPS-poorten (80 en 443), ongeacht Hallo **poort van oorsprong**.</span><span class="sxs-lookup"><span data-stu-id="f5271-141">hello endpoint itself will only be available tooend clients on hello default HTTP and HTTPS ports (80 and 443), regardless of hello **Origin port**.</span></span>  
   > 
   > <span data-ttu-id="f5271-142">**Azure CDN van Akamai** eindpunten Hallo volledige TCP-poortbereik voor oorsprongen niet toestaan.</span><span class="sxs-lookup"><span data-stu-id="f5271-142">**Azure CDN from Akamai** endpoints do not allow hello full TCP port range for origins.</span></span>  <span data-ttu-id="f5271-143">Zie [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx) (Door Azure CDN van Akamai toegestane poorten van oorsprong) voor een lijst met poorten van oorsprong die niet zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="f5271-143">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span></span>  
   > 
   > <span data-ttu-id="f5271-144">Toegang tot CDN-inhoud via HTTPS gelden Hallo volgende beperkingen:</span><span class="sxs-lookup"><span data-stu-id="f5271-144">Accessing CDN content using HTTPS has hello following constraints:</span></span>
   > 
   > * <span data-ttu-id="f5271-145">U moet Hallo opgegeven door Hallo CDN SSL-certificaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f5271-145">You must use hello SSL certificate provided by hello CDN.</span></span> <span data-ttu-id="f5271-146">Certificaten van derden worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="f5271-146">Third party certificates are not supported.</span></span>
   > * <span data-ttu-id="f5271-147">Moet u Hallo opgegeven CDN-domein (`<endpointname>.azureedge.net`) tooaccess HTTPS-inhoud.</span><span class="sxs-lookup"><span data-stu-id="f5271-147">You must use hello CDN-provided domain (`<endpointname>.azureedge.net`) tooaccess HTTPS content.</span></span> <span data-ttu-id="f5271-148">HTTPS-ondersteuning is niet beschikbaar voor aangepaste domeinnamen (CNAME's), aangezien Hallo CDN biedt geen ondersteuning voor aangepaste certificaten op dit moment.</span><span class="sxs-lookup"><span data-stu-id="f5271-148">HTTPS support is not available for custom domain names (CNAMEs) since hello CDN does not support custom certificates at this time.</span></span>
   > 
   > 
9. <span data-ttu-id="f5271-149">Klik op Hallo **toevoegen** knop toocreate Hallo nieuw eindpunt.</span><span class="sxs-lookup"><span data-stu-id="f5271-149">Click hello **Add** button toocreate hello new endpoint.</span></span>
10. <span data-ttu-id="f5271-150">Zodra het Hallo-eindpunt is gemaakt, wordt deze weergegeven in een lijst met eindpunten voor Hallo-profiel.</span><span class="sxs-lookup"><span data-stu-id="f5271-150">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="f5271-151">Hallo lijstweergave kunt u zien Hallo URL toouse tooaccess in de cache opgeslagen inhoud, evenals Hallo brondomein.</span><span class="sxs-lookup"><span data-stu-id="f5271-151">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
    
    ![CDN-eindpunt][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > <span data-ttu-id="f5271-153">Hallo-eindpunt onmiddellijk worden niet beschikbaar voor gebruik, zoals het duurt voor Hallo registratie toopropagate via Hallo CDN.</span><span class="sxs-lookup"><span data-stu-id="f5271-153">hello endpoint will not immediately be available for use, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="f5271-154">Profielen van <b>Azure CDN van Akamai</b> worden doorgaans binnen één minuut doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="f5271-154">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="f5271-155">Profielen van <b>Azure CDN van Verizon</b> worden doorgaans binnen 90 minuten doorgegeven, maar in sommige gevallen kan dit langer duren.</span><span class="sxs-lookup"><span data-stu-id="f5271-155">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
    > 
    > <span data-ttu-id="f5271-156">Gebruikers die toouse Hallo CDN-domeinnaam proberen voordat Hallo-eindpuntconfiguratie is doorgegeven toohello POP's, ontvangen HTTP 404-responscodes.</span><span class="sxs-lookup"><span data-stu-id="f5271-156">Users who try toouse hello CDN domain name before hello endpoint configuration has propagated toohello POPs will receive HTTP 404 response codes.</span></span>  <span data-ttu-id="f5271-157">Zie [Problemen oplossen met CDN-eindpunten die 404-statusberichten retourneren](cdn-troubleshoot-endpoint.md) als u een paar uur nadat u uw eindpunt hebt gemaakt, nog steeds 404-responsberichten ontvangt.</span><span class="sxs-lookup"><span data-stu-id="f5271-157">If it's been several hours since you created your endpoint and you're still receiving 404 responses, please see [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md).</span></span>
    > 
    > 

## <a name="see-also"></a><span data-ttu-id="f5271-158">Zie ook</span><span class="sxs-lookup"><span data-stu-id="f5271-158">See Also</span></span>
* [<span data-ttu-id="f5271-159">Het cachegedrag van aanvragen beheren met queryreeksen</span><span class="sxs-lookup"><span data-stu-id="f5271-159">Controlling caching behavior of requests with query strings</span></span>](cdn-query-string.md)
* [<span data-ttu-id="f5271-160">Hoe tooMap CDN inhoud tooa aangepaste domeinen</span><span class="sxs-lookup"><span data-stu-id="f5271-160">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="f5271-161">Vooraf assets op een Azure CDN-eindpunt laden</span><span class="sxs-lookup"><span data-stu-id="f5271-161">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="f5271-162">Een Azure CDN-eindpunt leegmaken</span><span class="sxs-lookup"><span data-stu-id="f5271-162">Purge an Azure CDN Endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="f5271-163">Problemen oplossen voor CDN-eindpunten die 404-statusberichten retourneren</span><span class="sxs-lookup"><span data-stu-id="f5271-163">Troubleshooting CDN endpoints returning 404 statuses</span></span>](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
