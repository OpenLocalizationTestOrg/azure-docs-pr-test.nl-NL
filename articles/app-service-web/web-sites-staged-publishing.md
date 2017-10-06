---
title: aaaSet up faseringsomgevingen voor web-apps in Azure App Service | Microsoft Docs
description: Meer informatie over hoe toouse gefaseerde publiceren voor web-apps in Azure App Service.
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="08d70-103">Faseringsomgevingen in Azure App Service instellen</span><span class="sxs-lookup"><span data-stu-id="08d70-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="08d70-104">Wanneer u implementeert uw web-app, web-app op Linux-, mobiele back-end- en API-app te[App Service](http://go.microsoft.com/fwlink/?LinkId=529714), u kunt afzonderlijke implementatiesleuf tooa in plaats van Hallo standaard productiesite implementeren bij uitvoering in Hallo **standaard**of **Premium** modus van App Service-plan.</span><span class="sxs-lookup"><span data-stu-id="08d70-104">When you deploy your web app, web app on Linux, mobile back end, and API app too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy tooa separate deployment slot instead of hello default production slot when running in hello **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="08d70-105">Implementatiesites zijn daadwerkelijk live apps met hun eigen hostnamen.</span><span class="sxs-lookup"><span data-stu-id="08d70-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="08d70-106">App-inhoud en configuratie-elementen worden ingewisseld tussen twee implementatiesites, met inbegrip van Hallo productiesite.</span><span class="sxs-lookup"><span data-stu-id="08d70-106">App content and configurations elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="08d70-107">Implementatie van de implementatiesleuf van uw toepassing tooa heeft Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="08d70-107">Deploying your application tooa deployment slot has hello following benefits:</span></span>

* <span data-ttu-id="08d70-108">U kunt appwijzigingen in een gefaseerde installatie implementatiesleuf valideren voordat het wisselen met Hallo productiesite.</span><span class="sxs-lookup"><span data-stu-id="08d70-108">You can validate app changes in a staging deployment slot before swapping it with hello production slot.</span></span>
* <span data-ttu-id="08d70-109">Een app tooa sleuf eerst implementeren en deze in productie wisselen zorgt u ervoor dat alle exemplaren van Hallo sleuf voordat gewisseld naar de productie zijn opgewarmd.</span><span class="sxs-lookup"><span data-stu-id="08d70-109">Deploying an app tooa slot first and swapping it into production ensures that all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="08d70-110">Hierdoor is er uitvaltijd wanneer u uw app implementeert.</span><span class="sxs-lookup"><span data-stu-id="08d70-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="08d70-111">Hallo verkeer omleiden naadloze is en er zijn geen aanvragen worden verwijderd als gevolg van de wisseling bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="08d70-111">hello traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="08d70-112">Deze volledige werkstroom kan worden geautomatiseerd door configureren [automatisch wisselen](#Auto-Swap) wanneer vooraf swap-validatie is niet nodig.</span><span class="sxs-lookup"><span data-stu-id="08d70-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="08d70-113">Als een wisseling heeft Hallo sleuf met eerder voorbereide app Hallo vorige productie-app.</span><span class="sxs-lookup"><span data-stu-id="08d70-113">After a swap, hello slot with previously staged app now has hello previous production app.</span></span> <span data-ttu-id="08d70-114">Als gewisseld naar de productiesite Hallo Hallo-wijzigingen zijn niet zoals u verwacht, kunt u dezelfde wisselen onmiddellijk back-tooget uw "laatst bekende goede site" hello uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="08d70-114">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good site" back.</span></span>

<span data-ttu-id="08d70-115">Elke App Service plan modus ondersteunt een verschillend aantal implementatiesites.</span><span class="sxs-lookup"><span data-stu-id="08d70-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="08d70-116">toofind hello aantal sleuven van uw app-modus ondersteunt, Zie [prijzen van App Service](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="08d70-116">toofind out hello number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="08d70-117">Wanneer uw app meerdere sleuven heeft, kunt u het Hallo-modus niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="08d70-117">When your app has multiple slots, you cannot change hello mode.</span></span>
* <span data-ttu-id="08d70-118">Schalen is niet beschikbaar voor niet-productieve sleuven.</span><span class="sxs-lookup"><span data-stu-id="08d70-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="08d70-119">Gekoppelde bronbeheer wordt niet ondersteund voor niet-productieve sleuven.</span><span class="sxs-lookup"><span data-stu-id="08d70-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="08d70-120">In Hallo [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) u kunt dit mogelijk invloed op een productiesite alleen voorkomen door het Hallo niet productiesite tooa App Service plan modus tijdelijk te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="08d70-120">In hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving hello non-production slot tooa different App Service plan mode.</span></span> <span data-ttu-id="08d70-121">Opmerking die niet-productieve Hallo sleuf moet Hallo nogmaals delen dezelfde modus met Hallo productiesite voordat u kunt twee Hallo sleuven omwisselen.</span><span class="sxs-lookup"><span data-stu-id="08d70-121">Note that hello non-production slot must once again share hello same mode with hello production slot before you can swap hello two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="08d70-122">Een implementatiesleuf toevoegen</span><span class="sxs-lookup"><span data-stu-id="08d70-122">Add a deployment slot</span></span>
<span data-ttu-id="08d70-123">Hallo-app moet worden uitgevoerd in Hallo **standaard** of **Premium** modus in volgorde voor u tooenable meerdere implementatiesites.</span><span class="sxs-lookup"><span data-stu-id="08d70-123">hello app must be running in hello **Standard** or **Premium** mode in order for you tooenable multiple deployment slots.</span></span>

1. <span data-ttu-id="08d70-124">In Hallo [Azure Portal](https://portal.azure.com/), opent u uw app [resourceblade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="08d70-124">In hello [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="08d70-125">Kies Hallo **implementatiesites** optie en klik vervolgens op **sleuf toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="08d70-125">Choose hello **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![Voeg een nieuwe implementatiesleuf][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="08d70-127">Als Hallo app nog niet Hallo **standaard** of **Premium** modus, ontvangt u een bericht weergegeven dat aangeeft Hallo ondersteund modi voor het inschakelen van voorbereide publiceren.</span><span class="sxs-lookup"><span data-stu-id="08d70-127">If hello app is not already in hello **Standard** or **Premium** mode, you will receive a message indicating hello supported modes for enabling staged publishing.</span></span> <span data-ttu-id="08d70-128">Op dit moment hebt u Hallo optie tooselect **Upgrade** en navigeer toohello **Scale** tabblad van uw app voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="08d70-128">At this point, you have hello option tooselect **Upgrade** and navigate toohello **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="08d70-129">In Hallo **toevoegen van een sleuf** blade Hallo sleuf een naam geven en selecteer of tooclone app configuratie uit een andere bestaande implementatiesleuf.</span><span class="sxs-lookup"><span data-stu-id="08d70-129">In hello **Add a slot** blade, give hello slot a name, and select whether tooclone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="08d70-130">Klik op Hallo vinkje toocontinue.</span><span class="sxs-lookup"><span data-stu-id="08d70-130">Click hello check mark toocontinue.</span></span>
   
    ![Configuratiebron][ConfigurationSource1]
   
    <span data-ttu-id="08d70-132">Hallo eerste keer dat u een site toevoegen wordt alleen hebt u twee mogelijkheden: configuratie van de kloon uit Hallo standaard sleuf in productie of helemaal niet.</span><span class="sxs-lookup"><span data-stu-id="08d70-132">hello first time you add a slot, you will only have two choices: clone configuration from hello default slot in production or not at all.</span></span>
    <span data-ttu-id="08d70-133">Wanneer u meerdere sleuven hebt gemaakt, kunt u zich kunt tooclone configuratie uit een sleuf dan Hallo in productie:</span><span class="sxs-lookup"><span data-stu-id="08d70-133">After you have created several slots, you will be able tooclone configuration from a slot other than hello one in production:</span></span>
   
    ![Configuratie van bronnen][MultipleConfigurationSources]
4. <span data-ttu-id="08d70-135">Klik in de resourceblade van de app, op **implementatiesites**, klikt u vervolgens op een implementatiesleuf tooopen die sleuf resource-blade met een set van metrische gegevens en configuratie net als elke andere app.</span><span class="sxs-lookup"><span data-stu-id="08d70-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot tooopen that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="08d70-136">Hallo naam van Hallo sleuf weergegeven bovenaan Hallo Hallo blade tooremind u die u bekijkt implementatiesleuf Hallo.</span><span class="sxs-lookup"><span data-stu-id="08d70-136">hello name of hello slot is shown at hello top of hello blade tooremind you that you are viewing hello deployment slot.</span></span>
   
    ![Implementatiesleuf titel][StagingTitle]
5. <span data-ttu-id="08d70-138">Klik op Hallo app-URL in de blade Hallo-sleuf.</span><span class="sxs-lookup"><span data-stu-id="08d70-138">Click hello app URL in hello slot's blade.</span></span> <span data-ttu-id="08d70-139">Kennisgeving Hallo implementatiesleuf heeft een eigen hostnaam en is ook een live-app.</span><span class="sxs-lookup"><span data-stu-id="08d70-139">Notice hello deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="08d70-140">toolimit openbare toegang toohello implementatiesleuf Zie [App Service Web-App – blok web access toonon productie-implementatiesites](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span><span class="sxs-lookup"><span data-stu-id="08d70-140">toolimit public access toohello deployment slot, see [App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="08d70-141">Er is geen inhoud nadat de implementatiesleuf is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="08d70-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="08d70-142">U kunt toohello sleuf vanaf een andere opslagplaats vertakking of een geheel andere opslagplaats implementeren.</span><span class="sxs-lookup"><span data-stu-id="08d70-142">You can deploy toohello slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="08d70-143">U kunt ook Hallo siteconfiguratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="08d70-143">You can also change hello slot's configuration.</span></span> <span data-ttu-id="08d70-144">Gebruik Hallo publiceren of de implementatie-referenties die zijn gekoppeld aan de implementatiesleuf Hallo voor updates van inhoud.</span><span class="sxs-lookup"><span data-stu-id="08d70-144">Use hello publish profile or deployment credentials associated with hello deployment slot for content updates.</span></span>  <span data-ttu-id="08d70-145">U kunt bijvoorbeeld [toothis sleuf met git publiceren](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="08d70-145">For example, you can [publish toothis slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="08d70-146">Configuratie voor implementatiesites</span><span class="sxs-lookup"><span data-stu-id="08d70-146">Configuration for deployment slots</span></span>
<span data-ttu-id="08d70-147">Als u een configuratie uit een andere implementatiesleuf kloon is Hallo gekloonde configuratie kan worden bewerkt.</span><span class="sxs-lookup"><span data-stu-id="08d70-147">When you clone configuration from another deployment slot, hello cloned configuration is editable.</span></span> <span data-ttu-id="08d70-148">Bovendien volgen sommige configuratie-elementen Hallo inhoud via een wisseling (kan niet in sleuf worden specifieke) terwijl andere configuratie-elementen blijft in Hallo dezelfde sleuf na een wisseling (sleuf specifieke).</span><span class="sxs-lookup"><span data-stu-id="08d70-148">Furthermore, some configuration elements will follow hello content across a swap (not slot specific) while other configuration elements will stay in hello same slot after a swap (slot specific).</span></span> <span data-ttu-id="08d70-149">Hallo ziet volgende lijsten Hallo-configuratie die wordt gewijzigd wanneer u sleuven wisselen.</span><span class="sxs-lookup"><span data-stu-id="08d70-149">hello following lists show hello configuration that will change when you swap slots.</span></span>

<span data-ttu-id="08d70-150">**Instellingen die worden omgewisseld**:</span><span class="sxs-lookup"><span data-stu-id="08d70-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="08d70-151">Algemene instellingen - zoals framework-versie, 64-32-bits, Web-sockets</span><span class="sxs-lookup"><span data-stu-id="08d70-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="08d70-152">App-instellingen (kan worden geconfigureerd toostick tooa sleuf)</span><span class="sxs-lookup"><span data-stu-id="08d70-152">App settings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="08d70-153">Verbindingsreeksen (kan worden geconfigureerd toostick tooa sleuf)</span><span class="sxs-lookup"><span data-stu-id="08d70-153">Connection strings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="08d70-154">Handlertoewijzingen</span><span class="sxs-lookup"><span data-stu-id="08d70-154">Handler mappings</span></span>
* <span data-ttu-id="08d70-155">Instellingen voor controle en diagnose</span><span class="sxs-lookup"><span data-stu-id="08d70-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="08d70-156">WebJobs-inhoud</span><span class="sxs-lookup"><span data-stu-id="08d70-156">WebJobs content</span></span>

<span data-ttu-id="08d70-157">**Instellingen die niet worden omgewisseld**:</span><span class="sxs-lookup"><span data-stu-id="08d70-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="08d70-158">Publicatie-eindpunten</span><span class="sxs-lookup"><span data-stu-id="08d70-158">Publishing endpoints</span></span>
* <span data-ttu-id="08d70-159">Aangepaste domeinnamen</span><span class="sxs-lookup"><span data-stu-id="08d70-159">Custom Domain Names</span></span>
* <span data-ttu-id="08d70-160">SSL-certificaten en bindingen</span><span class="sxs-lookup"><span data-stu-id="08d70-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="08d70-161">Schaalinstellingen</span><span class="sxs-lookup"><span data-stu-id="08d70-161">Scale settings</span></span>
* <span data-ttu-id="08d70-162">WebJobs planners</span><span class="sxs-lookup"><span data-stu-id="08d70-162">WebJobs schedulers</span></span>

<span data-ttu-id="08d70-163">een instelling of verbinding tekenreeks toostick tooa appsite (geen verwisseld) toegang Hallo tooconfigure **toepassingsinstellingen** blade voor een specifieke site en vervolgens selecteert Hallo **sleuf instelling** in voor Hallo configuratie-elementen die Hallo sleuf moeten houden.</span><span class="sxs-lookup"><span data-stu-id="08d70-163">tooconfigure an app setting or connection string toostick tooa slot (not swapped), access hello **Application Settings** blade for a specific slot, then select hello **Slot Setting** box for hello configuration elements that should stick hello slot.</span></span> <span data-ttu-id="08d70-164">Houd er rekening mee dat een configuratie-element als gemarkeerd sleuf specifieke heeft Hallo effect van het tot stand brengen van dat element als niet verwisselbare over alle Hallo implementatiesites Hallo app gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="08d70-164">Note that marking a configuration element as slot specific has hello effect of establishing that element as not swappable across all hello deployment slots associated with hello app.</span></span>

![Sleufinstellingen][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="08d70-166">Wisselen implementatiesites</span><span class="sxs-lookup"><span data-stu-id="08d70-166">Swap deployment slots</span></span> 
<span data-ttu-id="08d70-167">U kunt wisselen implementatiesites in Hallo **overzicht** of **implementatiesites** weergave van de resource-blade van uw app.</span><span class="sxs-lookup"><span data-stu-id="08d70-167">You can swap deployment slots in hello **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08d70-168">Voordat u een app van een implementatiesleuf naar de productie wisselen, zorg ervoor dat alle niet-specifieke sleufinstellingen precies zoals u wilt dat toohave zijn geconfigureerd in Hallo wisselen doel.</span><span class="sxs-lookup"><span data-stu-id="08d70-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want toohave it in hello swap target.</span></span>
> 
> 

1. <span data-ttu-id="08d70-169">tooswap implementatiesites, klikt u op Hallo **wisselen** knop in de opdrachtbalk Hallo van Hallo app of in de opdrachtbalk Hallo van een implementatiesleuf.</span><span class="sxs-lookup"><span data-stu-id="08d70-169">tooswap deployment slots, click hello **Swap** button in hello command bar of hello app or in hello command bar of a deployment slot.</span></span>
   
    ![Knop wisselen][SwapButtonBar]

2. <span data-ttu-id="08d70-171">Zorg ervoor dat Hallo wisselen bron- en wisselen doel correct zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="08d70-171">Make sure that hello swap source and swap target are set properly.</span></span> <span data-ttu-id="08d70-172">Hallo wisselen doel is meestal Hallo productiesite.</span><span class="sxs-lookup"><span data-stu-id="08d70-172">Usually, hello swap target is hello production slot.</span></span> <span data-ttu-id="08d70-173">Klik op **OK** toocomplete Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="08d70-173">Click **OK** toocomplete hello operation.</span></span> <span data-ttu-id="08d70-174">Wanneer het Hallo-bewerking is voltooid, hebt Hallo implementatiesites zijn gewisseld.</span><span class="sxs-lookup"><span data-stu-id="08d70-174">When hello operation finishes, hello deployment slots have been swapped.</span></span>

    ![Wisseling voltooien](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="08d70-176">Voor Hallo **wisseling met voorbeeld** type wisselen, Zie [wisseling met voorbeeld (meerdere fase swap)](#Multi-Phase).</span><span class="sxs-lookup"><span data-stu-id="08d70-176">For hello **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="08d70-177">Wisselen met voorbeeld (meerdere fase swap)</span><span class="sxs-lookup"><span data-stu-id="08d70-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="08d70-178">Wisselen met voorbeeld of meerdere stap wisseling, validatie van de site-specifieke configuratie-elementen, zoals verbindingsreeksen vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="08d70-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="08d70-179">Bedrijfskritieke werkbelastingen gewenste toovalidate die Hallo app werkt zoals verwacht tijdens het Hallo-productiesite van configuratie is toegepast en moet u deze validatie uitvoeren *voordat* Hallo-app wordt gewisseld naar de productie.</span><span class="sxs-lookup"><span data-stu-id="08d70-179">For mission-critical workloads, you want toovalidate that hello app behaves as expected when hello production slot's configuration is applied, and you must perform such validation *before* hello app is swapped into production.</span></span> <span data-ttu-id="08d70-180">Wisseling met voorbeeld is wat u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="08d70-180">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="08d70-181">Wisseling met voorbeeld wordt niet ondersteund in web-apps op Linux.</span><span class="sxs-lookup"><span data-stu-id="08d70-181">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="08d70-182">Wanneer u Hallo gebruikt **wisselen met voorbeeld** optie (Zie [implementatiesites wisselen](#Swap)), App Service Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="08d70-182">When you use hello **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does hello following:</span></span>

- <span data-ttu-id="08d70-183">Houdt Hallo bestemming sleuf ongewijzigd zodat bestaande werkbelasting op die sleuf (bijvoorbeeld productie) wordt niet beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="08d70-183">Keeps hello destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="08d70-184">Van toepassing hello configuratie-elementen van Hallo sleuf toohello bron doelsleuf, met inbegrip van Hallo sleuf-specifieke verbindingsreeksen en app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="08d70-184">Applies hello configuration elements of hello destination slot toohello source slot, including hello slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="08d70-185">Hallo werkprocessen op Hallo bron sleuf met behulp van deze elementen van de hiervoor genoemde configuratie opnieuw is opgestart.</span><span class="sxs-lookup"><span data-stu-id="08d70-185">Restarts hello worker processes on hello source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="08d70-186">Wanneer u Hallo wisseling voltooien: verplaatst Hallo pre-warmed-up bronsite in Hallo doelsleuf.</span><span class="sxs-lookup"><span data-stu-id="08d70-186">When you complete hello swap: Moves hello pre-warmed-up source slot into hello destination slot.</span></span> <span data-ttu-id="08d70-187">Hallo doelsleuf verplaatst naar het Hallo-bronsite als een handmatige wisseling in.</span><span class="sxs-lookup"><span data-stu-id="08d70-187">hello destination slot is moved into hello source slot as in a manual swap.</span></span>
- <span data-ttu-id="08d70-188">Wanneer u annuleert Hallo wisselen: Hallo-configuratie-elementen van Hallo bron sleuf toohello bron sleuf past.</span><span class="sxs-lookup"><span data-stu-id="08d70-188">When you cancel hello swap: Reapplies hello configuration elements of hello source slot toohello source slot.</span></span>

<span data-ttu-id="08d70-189">U kunt een voorbeeld precies hoe Hallo-app met Hallo bestemming sleuf configuratie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="08d70-189">You can preview exactly how hello app will behave with hello destination slot's configuration.</span></span> <span data-ttu-id="08d70-190">Nadat de validatie is voltooid, kunt u Hallo wisseling in een aparte stap voltooien.</span><span class="sxs-lookup"><span data-stu-id="08d70-190">Once you complete validation, you complete hello swap in a separate step.</span></span> <span data-ttu-id="08d70-191">Deze stap is Hallo bijkomend voordeel dat Hallo bron sleuf al met de gewenste configuratie Hallo opgewarmd en clients niet geen downtime ondervinden wordt.</span><span class="sxs-lookup"><span data-stu-id="08d70-191">This step has hello added advantage that hello source slot is already warmed up with hello desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="08d70-192">Voorbeelden voor hello Azure PowerShell-cmdlets voor meerdere stap wisseling zijn opgenomen in hello Azure PowerShell-cmdlets voor implementatie sleuven sectie.</span><span class="sxs-lookup"><span data-stu-id="08d70-192">Samples for hello Azure PowerShell cmdlets available for multi-phase swap are included in hello Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="08d70-193">Automatisch wisselen configureren</span><span class="sxs-lookup"><span data-stu-id="08d70-193">Configure Auto Swap</span></span>
<span data-ttu-id="08d70-194">Uw app met nul koude start en uitvaltijd implementeren automatisch wisselen zodat DevOps-scenario's waar u toocontinuously wilt voor end-klanten van Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="08d70-194">Auto Swap streamlines DevOps scenarios where you want toocontinuously deploy your app with zero cold start and zero downtime for end customers of hello app.</span></span> <span data-ttu-id="08d70-195">Wanneer een implementatiesleuf is geconfigureerd voor automatisch wisselen naar de productie, elke keer dat u uw code update toothat sleuf pushen, wordt App Service automatisch Hallo app wisselen naar de productie nadat deze al is opgewarmd in sleuf Hallo.</span><span class="sxs-lookup"><span data-stu-id="08d70-195">When a deployment slot is configured for Auto Swap into production, every time you push your code update toothat slot, App Service will automatically swap hello app into production after it has already warmed up in hello slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08d70-196">Wanneer u automatisch wisselen voor een site inschakelt, zorg ervoor dat siteconfiguratie Hallo exact Hallo configuratie is bedoeld voor Hallo doel sleuf (meestal Hallo productiesite).</span><span class="sxs-lookup"><span data-stu-id="08d70-196">When you enable Auto Swap for a slot, make sure hello slot configuration is exactly hello configuration intended for hello target slot (usually hello production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="08d70-197">Automatisch wisselen wordt niet ondersteund in web-apps op Linux.</span><span class="sxs-lookup"><span data-stu-id="08d70-197">Auto swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="08d70-198">Automatisch wisselen configureren voor een sleuf is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="08d70-198">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="08d70-199">Volg onderstaande stappen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="08d70-199">Follow hello steps below:</span></span>

1. <span data-ttu-id="08d70-200">In **Implementatiesites**, selecteert u een niet-productiesite en kiest u **toepassingsinstellingen** in die sleuf resource-blade.</span><span class="sxs-lookup"><span data-stu-id="08d70-200">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="08d70-201">Selecteer **op** voor **automatisch wisselen**, selecteer Hallo gewenste doel sleuf in **automatisch wisselen sleuf**, en klik op **opslaan** in de opdrachtbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="08d70-201">Select **On** for **Auto Swap**, select hello desired target slot in **Auto Swap Slot**, and click **Save** in hello command bar.</span></span> <span data-ttu-id="08d70-202">Zorg ervoor dat de configuratie voor Hallo sleuf exact Hallo configuratie is bedoeld voor Hallo doel sleuf.</span><span class="sxs-lookup"><span data-stu-id="08d70-202">Make sure configuration for hello slot is exactly hello configuration intended for hello target slot.</span></span>
   
    <span data-ttu-id="08d70-203">Hallo **meldingen** tabblad knippert een groene **geslaagd** zodra het Hallo-bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="08d70-203">hello **Notifications** tab will flash a green **SUCCESS** once hello operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="08d70-204">tootest automatisch wisselen voor uw app, kunt u eerst een niet-productieve doel sleuf in selecteren **automatisch wisselen sleuf** toobecome bekend bent met het Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="08d70-204">tootest Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** toobecome familiar with hello feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="08d70-205">Een implementatiesleuf code push toothat uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="08d70-205">Execute a code push toothat deployment slot.</span></span> <span data-ttu-id="08d70-206">Automatisch wisselen gebeurt na een korte periode en Hallo update, worden weergegeven op de doel-sleuf URL.</span><span class="sxs-lookup"><span data-stu-id="08d70-206">Auto Swap will happen after a short time and hello update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a><span data-ttu-id="08d70-207">toorollback een productie-app na wisselen</span><span class="sxs-lookup"><span data-stu-id="08d70-207">toorollback a production app after swap</span></span>
<span data-ttu-id="08d70-208">Als er fouten worden geïdentificeerd in het nadat een wisseling sleuf, rollover van Hallo sleuven back tootheir vooraf wisselen statussen door Hallo dezelfde twee sleuven onmiddellijk wisselen.</span><span class="sxs-lookup"><span data-stu-id="08d70-208">If any errors are identified in production after a slot swap, roll hello slots back tootheir pre-swap states by swapping hello same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="08d70-209">Aangepaste opgewarmd voordat wisselen</span><span class="sxs-lookup"><span data-stu-id="08d70-209">Custom warm-up before swap</span></span>
<span data-ttu-id="08d70-210">Sommige apps mogelijk aangepaste opgewarmd acties.</span><span class="sxs-lookup"><span data-stu-id="08d70-210">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="08d70-211">Hallo `applicationInitialization` configuratie-element in web.config-bestand kunt u toospecify aangepaste initialisatie met acties toobe uitgevoerd voordat een aanvraag wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="08d70-211">hello `applicationInitialization` configuration element in web.config allows you toospecify custom initialization actions toobe performed before a request is received.</span></span> <span data-ttu-id="08d70-212">het wisselen van Hallo wacht tot deze toocomplete aangepaste opgewarmd.</span><span class="sxs-lookup"><span data-stu-id="08d70-212">hello swap operation will wait for this custom warm-up toocomplete.</span></span> <span data-ttu-id="08d70-213">Hier volgt een voorbeeld web.config fragment.</span><span class="sxs-lookup"><span data-stu-id="08d70-213">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a><span data-ttu-id="08d70-214">toodelete een implementatiesleuf</span><span class="sxs-lookup"><span data-stu-id="08d70-214">toodelete a deployment slot</span></span>
<span data-ttu-id="08d70-215">Hallo-blade voor een implementatiesleuf, open Hallo implementatiesleuf blade, klikt u op **overzicht** (Hallo standaardpagina) en klik op **verwijderen** in de opdrachtbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="08d70-215">In hello blade for a deployment slot, open hello deployment slot's blade, click **Overview** (hello default page), and click **Delete** in hello command bar.</span></span>  

![Een Implementatiesleuf verwijderen][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="08d70-217">Azure PowerShell-cmdlets voor implementatiesites</span><span class="sxs-lookup"><span data-stu-id="08d70-217">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="08d70-218">Azure PowerShell is een module die cmdlets toomanage Azure via Windows PowerShell, inclusief ondersteuning voor het beheren van implementatiesites in Azure App Service biedt.</span><span class="sxs-lookup"><span data-stu-id="08d70-218">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="08d70-219">Zie voor informatie over het installeren en configureren van Azure PowerShell, en Azure PowerShell verifiëren met uw Azure-abonnement, [hoe tooinstall en configureren van Microsoft Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="08d70-219">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How tooinstall and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="08d70-220">Een webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="08d70-220">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="08d70-221">Een implementatiesleuf te maken</span><span class="sxs-lookup"><span data-stu-id="08d70-221">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a><span data-ttu-id="08d70-222">Initieert een wisseling met revisie (meerdere fase swap) en doelsleuf sleuf configuratie toosource toepassen</span><span class="sxs-lookup"><span data-stu-id="08d70-222">Initiate a swap with review (multi-phase swap) and apply destination slot configuration toosource slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="08d70-223">Annuleren van een wisseling in behandeling (swap met revisie) en bron siteconfiguratie herstellen</span><span class="sxs-lookup"><span data-stu-id="08d70-223">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="08d70-224">Wisselen implementatiesites</span><span class="sxs-lookup"><span data-stu-id="08d70-224">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="08d70-225">Implementatiesite verwijderen</span><span class="sxs-lookup"><span data-stu-id="08d70-225">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="08d70-226">Azure Command-Line Interface (Azure CLI)-opdrachten voor Implementatiesites</span><span class="sxs-lookup"><span data-stu-id="08d70-226">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="08d70-227">Hello Azure CLI biedt platformoverschrijdende-opdrachten voor het werken met Azure, met inbegrip van ondersteuning voor het beheren van App Service-implementatiesites.</span><span class="sxs-lookup"><span data-stu-id="08d70-227">hello Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="08d70-228">Voor instructies over het installeren en configureren van hello Azure CLI, inclusief informatie over het tooconnect Azure CLI tooyour Azure-abonnement, Zie [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="08d70-228">For instructions on installing and configuring hello Azure CLI, including information on how tooconnect Azure CLI tooyour Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="08d70-229">toolist hello opdrachten die beschikbaar zijn voor Azure App Service in hello Azure CLI aanroepen `azure site -h`.</span><span class="sxs-lookup"><span data-stu-id="08d70-229">toolist hello commands available for Azure App Service in hello Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="08d70-230">Voor [Azure CLI 2.0](https://github.com/Azure/azure-cli) -opdrachten voor implementatiesites, Zie [az appservice web implementatiesleuf](/cli/azure/appservice/web/deployment/slot).</span><span class="sxs-lookup"><span data-stu-id="08d70-230">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="08d70-231">sitelijst voor Azure</span><span class="sxs-lookup"><span data-stu-id="08d70-231">azure site list</span></span>
<span data-ttu-id="08d70-232">Bel voor informatie over apps in het huidige abonnement Hallo Hallo **azure sitelijst**, Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="08d70-232">For information about hello apps in hello current subscription, call **azure site list**, as in hello following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="08d70-233">Azure site maken</span><span class="sxs-lookup"><span data-stu-id="08d70-233">azure site create</span></span>
<span data-ttu-id="08d70-234">aanroepen van een implementatiesleuf toocreate **azure site maken** en geeft Hallo-naam van een bestaande app en het Hallo-naam van Hallo sleuf toocreate, zoals in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="08d70-234">toocreate a deployment slot, call **azure site create** and specify hello name of an existing app and hello name of hello slot toocreate, as in hello following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="08d70-235">tooenable broncodebeheer voor Hallo nieuwe sleuf gebruik Hallo **--git** optie, zoals in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="08d70-235">tooenable source control for hello new slot, use hello **--git** option, as in hello following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="08d70-236">Azure site wisselen</span><span class="sxs-lookup"><span data-stu-id="08d70-236">azure site swap</span></span>
<span data-ttu-id="08d70-237">toomake Hallo bijgewerkte implementatiesleuf Hallo productie-app, gebruikt u Hallo **azure site wisselen** opdracht tooperform een wisselbewerking wordt uitgevoerd, zoals in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="08d70-237">toomake hello updated deployment slot hello production app, use hello **azure site swap** command tooperform a swap operation, as in hello following example.</span></span> <span data-ttu-id="08d70-238">Hallo productie-app wordt niet uitvaltijd ondervinden, noch wordt een koude start ondergaan.</span><span class="sxs-lookup"><span data-stu-id="08d70-238">hello production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="08d70-239">Azure site verwijderen</span><span class="sxs-lookup"><span data-stu-id="08d70-239">azure site delete</span></span>
<span data-ttu-id="08d70-240">toodelete een implementatiesleuf die niet langer nodig is, gebruik Hallo **azure site verwijderen** opdracht, zoals in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="08d70-240">toodelete a deployment slot that is no longer needed, use hello **azure site delete** command, as in hello following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="08d70-241">Bekijk een web-app in werking.</span><span class="sxs-lookup"><span data-stu-id="08d70-241">See a web app in action.</span></span> <span data-ttu-id="08d70-242">[App Service uitproberen](https://azure.microsoft.com/try/app-service/) onmiddellijk en maak een tijdelijke app: geen creditcard nodig en zonder verdere verplichtingen.</span><span class="sxs-lookup"><span data-stu-id="08d70-242">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="08d70-243">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="08d70-243">Next Steps</span></span>
<span data-ttu-id="08d70-244">[Azure App Service-Web App – blokkeren web access toonon productie implementatiesites](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[inleiding tooApp-Service op Linux](./app-service-linux-intro.md)
[gratis proefversie van Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="08d70-244">[Azure App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction tooApp Service on Linux](./app-service-linux-intro.md)
[Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

