---
title: Faseringsomgevingen voor web-apps in Azure App Service instellen | Microsoft Docs
description: Informatie over het gebruiken van voorbereide publiceren voor web-apps in Azure App Service.
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
ms.openlocfilehash: ca27c55eaaceb3109b1450c550330dfc416fdf55
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="25ff1-103">Faseringsomgevingen in Azure App Service instellen</span><span class="sxs-lookup"><span data-stu-id="25ff1-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="25ff1-104">Wanneer u uw web-app, web-app op Linux-, mobiele back-end- en API-app implementeert [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), u kunt implementeren op een afzonderlijke implementatiesleuf in plaats van de productiesite standaard bij uitvoering in de **standaard** of **Premium** modus van App Service-plan.</span><span class="sxs-lookup"><span data-stu-id="25ff1-104">When you deploy your web app, web app on Linux, mobile back end, and API app to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy to a separate deployment slot instead of the default production slot when running in the **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="25ff1-105">Implementatiesites zijn daadwerkelijk live apps met hun eigen hostnamen.</span><span class="sxs-lookup"><span data-stu-id="25ff1-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="25ff1-106">App-inhoud en configuratie-elementen worden ingewisseld tussen twee implementatiesites, met inbegrip van de productiesite.</span><span class="sxs-lookup"><span data-stu-id="25ff1-106">App content and configurations elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="25ff1-107">Uw toepassing om een implementatiesleuf te implementeren, heeft de volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="25ff1-107">Deploying your application to a deployment slot has the following benefits:</span></span>

* <span data-ttu-id="25ff1-108">U kunt appwijzigingen in een gefaseerde installatie implementatiesleuf valideren voordat het wisselen met de productiesite.</span><span class="sxs-lookup"><span data-stu-id="25ff1-108">You can validate app changes in a staging deployment slot before swapping it with the production slot.</span></span>
* <span data-ttu-id="25ff1-109">Zorgt ervoor dat alle exemplaren van de sleuf zijn opgewarmd voordat gewisseld naar de productie implementeert eerst een app in een sleuf en deze in productie te wisselen.</span><span class="sxs-lookup"><span data-stu-id="25ff1-109">Deploying an app to a slot first and swapping it into production ensures that all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="25ff1-110">Hierdoor is er uitvaltijd wanneer u uw app implementeert.</span><span class="sxs-lookup"><span data-stu-id="25ff1-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="25ff1-111">Het verkeer omleiden naadloze is en er zijn geen aanvragen worden verwijderd als gevolg van de wisseling bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="25ff1-111">The traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="25ff1-112">Deze volledige werkstroom kan worden geautomatiseerd door configureren [automatisch wisselen](#Auto-Swap) wanneer vooraf swap-validatie is niet nodig.</span><span class="sxs-lookup"><span data-stu-id="25ff1-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="25ff1-113">Als een wisseling heeft de sleuf met eerder voorbereide app de vorige productie-app.</span><span class="sxs-lookup"><span data-stu-id="25ff1-113">After a swap, the slot with previously staged app now has the previous production app.</span></span> <span data-ttu-id="25ff1-114">Als de gewisseld naar de productiesite wijzigingen zijn niet zoals u verwacht, kunt u de dezelfde swap onmiddellijk om uw "laatst bekende goede site" uitvoeren terug.</span><span class="sxs-lookup"><span data-stu-id="25ff1-114">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good site" back.</span></span>

<span data-ttu-id="25ff1-115">Elke App Service plan modus ondersteunt een verschillend aantal implementatiesites.</span><span class="sxs-lookup"><span data-stu-id="25ff1-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="25ff1-116">Sleuven om erachter te komen het nummer van uw app-modus ondersteunt, Zie [prijzen van App Service](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="25ff1-116">To find out the number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="25ff1-117">Wanneer uw app meerdere sleuven heeft, kunt u de modus niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="25ff1-117">When your app has multiple slots, you cannot change the mode.</span></span>
* <span data-ttu-id="25ff1-118">Schalen is niet beschikbaar voor niet-productieve sleuven.</span><span class="sxs-lookup"><span data-stu-id="25ff1-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="25ff1-119">Gekoppelde bronbeheer wordt niet ondersteund voor niet-productieve sleuven.</span><span class="sxs-lookup"><span data-stu-id="25ff1-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="25ff1-120">In de [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) u kunt dit mogelijk invloed op een productiesite alleen voorkomen door het tijdelijk de-productiesite verplaatsen naar een andere modus voor App Service-plan.</span><span class="sxs-lookup"><span data-stu-id="25ff1-120">In the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving the non-production slot to a different App Service plan mode.</span></span> <span data-ttu-id="25ff1-121">Houd er rekening mee dat de niet-productiesite nogmaals dezelfde modus met de productiesite delen moet voordat u kunt de twee sleuven omwisselen.</span><span class="sxs-lookup"><span data-stu-id="25ff1-121">Note that the non-production slot must once again share the same mode with the production slot before you can swap the two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="25ff1-122">Een implementatiesleuf toevoegen</span><span class="sxs-lookup"><span data-stu-id="25ff1-122">Add a deployment slot</span></span>
<span data-ttu-id="25ff1-123">De app moet worden uitgevoerd in de **standaard** of **Premium** modus zodat u meerdere implementatiesites inschakelen.</span><span class="sxs-lookup"><span data-stu-id="25ff1-123">The app must be running in the **Standard** or **Premium** mode in order for you to enable multiple deployment slots.</span></span>

1. <span data-ttu-id="25ff1-124">In de [Azure Portal](https://portal.azure.com/), opent u uw app [resourceblade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="25ff1-124">In the [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="25ff1-125">Kies de **implementatiesites** optie en klik vervolgens op **sleuf toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="25ff1-125">Choose the **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![Voeg een nieuwe implementatiesleuf][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="25ff1-127">Als de app nog niet in de **standaard** of **Premium** modus, ontvangt u een bericht met de ondersteunde modi voor het inschakelen van voorbereide publiceren.</span><span class="sxs-lookup"><span data-stu-id="25ff1-127">If the app is not already in the **Standard** or **Premium** mode, you will receive a message indicating the supported modes for enabling staged publishing.</span></span> <span data-ttu-id="25ff1-128">Op dit moment hebt u de optie te selecteren **Upgrade** en navigeer naar de **Scale** tabblad van uw app voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="25ff1-128">At this point, you have the option to select **Upgrade** and navigate to the **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="25ff1-129">In de **toevoegen van een sleuf** blade een naam opgeven voor de sleuf en selecteren of u de configuratie van de app uit een andere bestaande implementatiesleuf klonen.</span><span class="sxs-lookup"><span data-stu-id="25ff1-129">In the **Add a slot** blade, give the slot a name, and select whether to clone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="25ff1-130">Klik op het vinkje om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="25ff1-130">Click the check mark to continue.</span></span>
   
    ![Configuratiebron][ConfigurationSource1]
   
    <span data-ttu-id="25ff1-132">De eerste keer dat u een site toevoegt, hebt u slechts twee mogelijkheden: configuratie van de kloon van de standaard-sleuf in productie of helemaal niet.</span><span class="sxs-lookup"><span data-stu-id="25ff1-132">The first time you add a slot, you will only have two choices: clone configuration from the default slot in production or not at all.</span></span>
    <span data-ttu-id="25ff1-133">Wanneer u meerdere sleuven hebt gemaakt, kunt u zich kunt kloon configuratie uit een sleuf dan die in productie:</span><span class="sxs-lookup"><span data-stu-id="25ff1-133">After you have created several slots, you will be able to clone configuration from a slot other than the one in production:</span></span>
   
    ![Configuratie van bronnen][MultipleConfigurationSources]
4. <span data-ttu-id="25ff1-135">Klik in de resourceblade van de app, op **implementatiesites**, klikt u vervolgens op een implementatiesleuf die sleuf resource om blade te openen, met een set van metrische gegevens en configuratie net als elke andere app.</span><span class="sxs-lookup"><span data-stu-id="25ff1-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot to open that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="25ff1-136">De naam van de site wordt weergegeven boven aan de blade om eraan te herinneren dat u de implementatiesleuf bekijkt.</span><span class="sxs-lookup"><span data-stu-id="25ff1-136">The name of the slot is shown at the top of the blade to remind you that you are viewing the deployment slot.</span></span>
   
    ![Implementatiesleuf titel][StagingTitle]
5. <span data-ttu-id="25ff1-138">Klik op de app-URL in de sleuf blade.</span><span class="sxs-lookup"><span data-stu-id="25ff1-138">Click the app URL in the slot's blade.</span></span> <span data-ttu-id="25ff1-139">U ziet de implementatiesleuf heeft een eigen hostnaam en is ook een live-app.</span><span class="sxs-lookup"><span data-stu-id="25ff1-139">Notice the deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="25ff1-140">Als u wilt beperken voor openbare toegang tot de implementatiesleuf, Zie [App Service Web-App – blok webtoegang tot niet-productieve implementatiesites](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span><span class="sxs-lookup"><span data-stu-id="25ff1-140">To limit public access to the deployment slot, see [App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="25ff1-141">Er is geen inhoud nadat de implementatiesleuf is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="25ff1-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="25ff1-142">U kunt implementeren op de sleuf van een andere opslagplaats vertakking of een geheel andere opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="25ff1-142">You can deploy to the slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="25ff1-143">U kunt ook de sleuf configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="25ff1-143">You can also change the slot's configuration.</span></span> <span data-ttu-id="25ff1-144">Publiceren of de implementatie referenties gebruiken die zijn gekoppeld aan de implementatiesleuf voor updates van inhoud.</span><span class="sxs-lookup"><span data-stu-id="25ff1-144">Use the publish profile or deployment credentials associated with the deployment slot for content updates.</span></span>  <span data-ttu-id="25ff1-145">U kunt bijvoorbeeld [publiceren naar deze sleuf met git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="25ff1-145">For example, you can [publish to this slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="25ff1-146">Configuratie voor implementatiesites</span><span class="sxs-lookup"><span data-stu-id="25ff1-146">Configuration for deployment slots</span></span>
<span data-ttu-id="25ff1-147">Als u een configuratie uit een andere implementatiesleuf kloon, kan de configuratie van de gekloonde worden bewerkt.</span><span class="sxs-lookup"><span data-stu-id="25ff1-147">When you clone configuration from another deployment slot, the cloned configuration is editable.</span></span> <span data-ttu-id="25ff1-148">Bepaalde configuratie-elementen wordt bovendien de inhoud via een wisseling (kan niet in sleuf worden specifieke) gevolgd terwijl andere configuratie-elementen staan in dezelfde sleuf zijn na een wisseling (sleuf specifieke blijft).</span><span class="sxs-lookup"><span data-stu-id="25ff1-148">Furthermore, some configuration elements will follow the content across a swap (not slot specific) while other configuration elements will stay in the same slot after a swap (slot specific).</span></span> <span data-ttu-id="25ff1-149">De volgende lijsten ziet de configuratie die wordt gewijzigd wanneer u sleuven wisselen.</span><span class="sxs-lookup"><span data-stu-id="25ff1-149">The following lists show the configuration that will change when you swap slots.</span></span>

<span data-ttu-id="25ff1-150">**Instellingen die worden omgewisseld**:</span><span class="sxs-lookup"><span data-stu-id="25ff1-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="25ff1-151">Algemene instellingen - zoals framework-versie, 64-32-bits, Web-sockets</span><span class="sxs-lookup"><span data-stu-id="25ff1-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="25ff1-152">App-instellingen (kan worden geconfigureerd om te blijven hangen in een sleuf)</span><span class="sxs-lookup"><span data-stu-id="25ff1-152">App settings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="25ff1-153">Verbindingsreeksen (kan worden geconfigureerd om te blijven hangen in een sleuf)</span><span class="sxs-lookup"><span data-stu-id="25ff1-153">Connection strings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="25ff1-154">Handlertoewijzingen</span><span class="sxs-lookup"><span data-stu-id="25ff1-154">Handler mappings</span></span>
* <span data-ttu-id="25ff1-155">Instellingen voor controle en diagnose</span><span class="sxs-lookup"><span data-stu-id="25ff1-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="25ff1-156">WebJobs-inhoud</span><span class="sxs-lookup"><span data-stu-id="25ff1-156">WebJobs content</span></span>

<span data-ttu-id="25ff1-157">**Instellingen die niet worden omgewisseld**:</span><span class="sxs-lookup"><span data-stu-id="25ff1-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="25ff1-158">Publicatie-eindpunten</span><span class="sxs-lookup"><span data-stu-id="25ff1-158">Publishing endpoints</span></span>
* <span data-ttu-id="25ff1-159">Aangepaste domeinnamen</span><span class="sxs-lookup"><span data-stu-id="25ff1-159">Custom Domain Names</span></span>
* <span data-ttu-id="25ff1-160">SSL-certificaten en bindingen</span><span class="sxs-lookup"><span data-stu-id="25ff1-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="25ff1-161">Schaalinstellingen</span><span class="sxs-lookup"><span data-stu-id="25ff1-161">Scale settings</span></span>
* <span data-ttu-id="25ff1-162">WebJobs planners</span><span class="sxs-lookup"><span data-stu-id="25ff1-162">WebJobs schedulers</span></span>

<span data-ttu-id="25ff1-163">Voor het configureren van een app-instelling of verbindingstekenreeks aan een site (niet verwisseld) toegang krijgen tot de **toepassingsinstellingen** blade voor een specifieke site, selecteer vervolgens de **sleuf instelling** in voor de configuratie elementen die de sleuf moeten houden.</span><span class="sxs-lookup"><span data-stu-id="25ff1-163">To configure an app setting or connection string to stick to a slot (not swapped), access the **Application Settings** blade for a specific slot, then select the **Slot Setting** box for the configuration elements that should stick the slot.</span></span> <span data-ttu-id="25ff1-164">Houd er rekening mee dat als is gemarkeerd, een configuratie-element sleuf specifieke heeft het effect van het tot stand brengen van dat element als niet verwisselbare over alle implementatiesites die zijn gekoppeld aan de app.</span><span class="sxs-lookup"><span data-stu-id="25ff1-164">Note that marking a configuration element as slot specific has the effect of establishing that element as not swappable across all the deployment slots associated with the app.</span></span>

![Sleufinstellingen][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="25ff1-166">Wisselen implementatiesites</span><span class="sxs-lookup"><span data-stu-id="25ff1-166">Swap deployment slots</span></span> 
<span data-ttu-id="25ff1-167">U kunt wisselen implementatiesites in de **overzicht** of **implementatiesites** weergave van de resource-blade van uw app.</span><span class="sxs-lookup"><span data-stu-id="25ff1-167">You can swap deployment slots in the **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25ff1-168">Voordat u een app van een implementatiesleuf naar de productie wisselen, zorg ervoor dat alle niet-specifieke sleufinstellingen precies zoals u wilt dat dit in de doel-wisseling zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="25ff1-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want to have it in the swap target.</span></span>
> 
> 

1. <span data-ttu-id="25ff1-169">Het wisselen van implementatiesites, klikt u op de **wisselen** knop in de opdrachtbalk van de app of in de opdrachtbalk van een implementatiesleuf.</span><span class="sxs-lookup"><span data-stu-id="25ff1-169">To swap deployment slots, click the **Swap** button in the command bar of the app or in the command bar of a deployment slot.</span></span>
   
    ![Knop wisselen][SwapButtonBar]

2. <span data-ttu-id="25ff1-171">Zorg ervoor dat de wisseling bron en het doel van de wisseling correct zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="25ff1-171">Make sure that the swap source and swap target are set properly.</span></span> <span data-ttu-id="25ff1-172">Het doel van de wisselruimte is meestal de productiesite.</span><span class="sxs-lookup"><span data-stu-id="25ff1-172">Usually, the swap target is the production slot.</span></span> <span data-ttu-id="25ff1-173">Klik op **OK** om de bewerking te voltooien.</span><span class="sxs-lookup"><span data-stu-id="25ff1-173">Click **OK** to complete the operation.</span></span> <span data-ttu-id="25ff1-174">Wanneer de bewerking is voltooid, hebben de implementatiesites zijn gewisseld.</span><span class="sxs-lookup"><span data-stu-id="25ff1-174">When the operation finishes, the deployment slots have been swapped.</span></span>

    ![Wisseling voltooien](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="25ff1-176">Voor de **wisseling met voorbeeld** type wisselen, Zie [wisseling met voorbeeld (meerdere fase swap)](#Multi-Phase).</span><span class="sxs-lookup"><span data-stu-id="25ff1-176">For the **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="25ff1-177">Wisselen met voorbeeld (meerdere fase swap)</span><span class="sxs-lookup"><span data-stu-id="25ff1-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="25ff1-178">Wisselen met voorbeeld of meerdere stap wisseling, validatie van de site-specifieke configuratie-elementen, zoals verbindingsreeksen vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="25ff1-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="25ff1-179">Bedrijfskritieke werkbelastingen, u wilt valideren dat de app werkt zoals verwacht wanneer de productiesite configuratie is toegepast en moet u deze validatie uitvoeren *voordat* de app wordt gewisseld naar de productie.</span><span class="sxs-lookup"><span data-stu-id="25ff1-179">For mission-critical workloads, you want to validate that the app behaves as expected when the production slot's configuration is applied, and you must perform such validation *before* the app is swapped into production.</span></span> <span data-ttu-id="25ff1-180">Wisseling met voorbeeld is wat u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="25ff1-180">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="25ff1-181">Wisseling met voorbeeld wordt niet ondersteund in web-apps op Linux.</span><span class="sxs-lookup"><span data-stu-id="25ff1-181">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="25ff1-182">Wanneer u gebruikt de **wisselen met voorbeeld** optie (Zie [implementatiesites wisselen](#Swap)), App Service doet het volgende:</span><span class="sxs-lookup"><span data-stu-id="25ff1-182">When you use the **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does the following:</span></span>

- <span data-ttu-id="25ff1-183">Houdt de doelsleuf ongewijzigd zodat bestaande werkbelasting op die sleuf (bijvoorbeeld productie) wordt niet negatief beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="25ff1-183">Keeps the destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="25ff1-184">Geldt de configuratie-elementen van de doelsleuf naar de bronsite, met inbegrip van de site-specifieke verbindingsreeksen en app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="25ff1-184">Applies the configuration elements of the destination slot to the source slot, including the slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="25ff1-185">De werkprocessen op de bronsite met behulp van deze elementen van de hiervoor genoemde configuratie opnieuw is opgestart.</span><span class="sxs-lookup"><span data-stu-id="25ff1-185">Restarts the worker processes on the source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="25ff1-186">Wanneer u de wisseling voltooien: de bron van de pre-warmed-up sleuf is verplaatst naar de doelsleuf.</span><span class="sxs-lookup"><span data-stu-id="25ff1-186">When you complete the swap: Moves the pre-warmed-up source slot into the destination slot.</span></span> <span data-ttu-id="25ff1-187">De doelsleuf wordt verplaatst naar de bronsite in een handmatige wisseling.</span><span class="sxs-lookup"><span data-stu-id="25ff1-187">The destination slot is moved into the source slot as in a manual swap.</span></span>
- <span data-ttu-id="25ff1-188">Wanneer u de swap annuleert: past u de configuratie-elementen van de bronsite naar de bronsite.</span><span class="sxs-lookup"><span data-stu-id="25ff1-188">When you cancel the swap: Reapplies the configuration elements of the source slot to the source slot.</span></span>

<span data-ttu-id="25ff1-189">U kunt een voorbeeld precies hoe de app wordt uitgevoerd met de configuratie van de doelsleuf.</span><span class="sxs-lookup"><span data-stu-id="25ff1-189">You can preview exactly how the app will behave with the destination slot's configuration.</span></span> <span data-ttu-id="25ff1-190">Nadat de validatie is voltooid, kunt u de wisselruimte in een aparte stap voltooien.</span><span class="sxs-lookup"><span data-stu-id="25ff1-190">Once you complete validation, you complete the swap in a separate step.</span></span> <span data-ttu-id="25ff1-191">Deze stap is de toegevoegde voordeel dat de bron-sleuf al met de gewenste configuratie opgewarmd en clients wordt niet ondervinden geen downtime.</span><span class="sxs-lookup"><span data-stu-id="25ff1-191">This step has the added advantage that the source slot is already warmed up with the desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="25ff1-192">Voorbeelden voor de Azure PowerShell-cmdlets beschikbaar voor meerdere stap wisseling zijn opgenomen in de Azure PowerShell-cmdlets voor implementatie sleuven sectie.</span><span class="sxs-lookup"><span data-stu-id="25ff1-192">Samples for the Azure PowerShell cmdlets available for multi-phase swap are included in the Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="25ff1-193">Automatisch wisselen configureren</span><span class="sxs-lookup"><span data-stu-id="25ff1-193">Configure Auto Swap</span></span>
<span data-ttu-id="25ff1-194">Automatisch wisselen stroomlijnt DevOps-scenario's waar u uw app met nul koude start en uitvaltijd continu implementeren voor klanten einde van de app.</span><span class="sxs-lookup"><span data-stu-id="25ff1-194">Auto Swap streamlines DevOps scenarios where you want to continuously deploy your app with zero cold start and zero downtime for end customers of the app.</span></span> <span data-ttu-id="25ff1-195">Wanneer een implementatiesleuf is geconfigureerd voor automatisch wisselen naar de productie, elke keer dat u de update-code pushen naar die sleuf, wordt App Service automatisch de app wisselen naar de productie nadat deze al in de sleuf is opgewarmd.</span><span class="sxs-lookup"><span data-stu-id="25ff1-195">When a deployment slot is configured for Auto Swap into production, every time you push your code update to that slot, App Service will automatically swap the app into production after it has already warmed up in the slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25ff1-196">Wanneer u automatisch wisselen voor een site inschakelt, zorg ervoor dat de configuratie van de implementatiesite exact de configuratie die bestemd zijn voor de doel-sleuf (meestal de productiesite).</span><span class="sxs-lookup"><span data-stu-id="25ff1-196">When you enable Auto Swap for a slot, make sure the slot configuration is exactly the configuration intended for the target slot (usually the production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="25ff1-197">Automatisch wisselen wordt niet ondersteund in web-apps op Linux.</span><span class="sxs-lookup"><span data-stu-id="25ff1-197">Auto swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="25ff1-198">Automatisch wisselen configureren voor een sleuf is eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="25ff1-198">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="25ff1-199">Volg de onderstaande stappen:</span><span class="sxs-lookup"><span data-stu-id="25ff1-199">Follow the steps below:</span></span>

1. <span data-ttu-id="25ff1-200">In **Implementatiesites**, selecteert u een niet-productiesite en kiest u **toepassingsinstellingen** in die sleuf resource-blade.</span><span class="sxs-lookup"><span data-stu-id="25ff1-200">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="25ff1-201">Selecteer **op** voor **automatisch wisselen**, selecteer de gewenste doel sleuf in **automatisch wisselen sleuf**, en klik op **opslaan** in de opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="25ff1-201">Select **On** for **Auto Swap**, select the desired target slot in **Auto Swap Slot**, and click **Save** in the command bar.</span></span> <span data-ttu-id="25ff1-202">Zorg ervoor dat de configuratie voor de sleuf exact de configuratie die bestemd zijn voor de doel-sleuf.</span><span class="sxs-lookup"><span data-stu-id="25ff1-202">Make sure configuration for the slot is exactly the configuration intended for the target slot.</span></span>
   
    <span data-ttu-id="25ff1-203">De **meldingen** tabblad knippert een groene **geslaagd** nadat de bewerking voltooid is.</span><span class="sxs-lookup"><span data-stu-id="25ff1-203">The **Notifications** tab will flash a green **SUCCESS** once the operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="25ff1-204">Als u wilt testen automatisch wisselen voor uw app, kunt u eerst een niet-productieve doel sleuf in selecteren **automatisch wisselen sleuf** om vertrouwd te raken met de functie.</span><span class="sxs-lookup"><span data-stu-id="25ff1-204">To test Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** to become familiar with the feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="25ff1-205">Een code te pushen naar de uitrolfase die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="25ff1-205">Execute a code push to that deployment slot.</span></span> <span data-ttu-id="25ff1-206">Automatisch wisselen gebeurt na een korte periode en de update, worden weergegeven op de doel-sleuf URL.</span><span class="sxs-lookup"><span data-stu-id="25ff1-206">Auto Swap will happen after a short time and the update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="to-rollback-a-production-app-after-swap"></a><span data-ttu-id="25ff1-207">Terug te draaien, een productie-app na wisselen</span><span class="sxs-lookup"><span data-stu-id="25ff1-207">To rollback a production app after swap</span></span>
<span data-ttu-id="25ff1-208">Als er fouten worden geïdentificeerd in het nadat een wisseling sleuf, terugdraaien de sleuven naar de staat van vóór wisselen door de dezelfde twee sleuven onmiddellijk wisselen.</span><span class="sxs-lookup"><span data-stu-id="25ff1-208">If any errors are identified in production after a slot swap, roll the slots back to their pre-swap states by swapping the same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="25ff1-209">Aangepaste opgewarmd voordat wisselen</span><span class="sxs-lookup"><span data-stu-id="25ff1-209">Custom warm-up before swap</span></span>
<span data-ttu-id="25ff1-210">Sommige apps mogelijk aangepaste opgewarmd acties.</span><span class="sxs-lookup"><span data-stu-id="25ff1-210">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="25ff1-211">De `applicationInitialization` configuratie-element in web.config-bestand kunt u opgeven van aangepaste initialisatie met acties worden uitgevoerd voordat een aanvraag wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="25ff1-211">The `applicationInitialization` configuration element in web.config allows you to specify custom initialization actions to be performed before a request is received.</span></span> <span data-ttu-id="25ff1-212">De wisselbewerking wacht tot deze aangepaste opgewarmd om te voltooien.</span><span class="sxs-lookup"><span data-stu-id="25ff1-212">The swap operation will wait for this custom warm-up to complete.</span></span> <span data-ttu-id="25ff1-213">Hier volgt een voorbeeld web.config fragment.</span><span class="sxs-lookup"><span data-stu-id="25ff1-213">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="to-delete-a-deployment-slot"></a><span data-ttu-id="25ff1-214">Een implementatiesleuf verwijderen</span><span class="sxs-lookup"><span data-stu-id="25ff1-214">To delete a deployment slot</span></span>
<span data-ttu-id="25ff1-215">In de blade voor een implementatiesleuf de implementatiesleuf blade geopend, klikt u op **overzicht** (de standaardpagina), en klik op **verwijderen** in de opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="25ff1-215">In the blade for a deployment slot, open the deployment slot's blade, click **Overview** (the default page), and click **Delete** in the command bar.</span></span>  

![Een Implementatiesleuf verwijderen][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="25ff1-217">Azure PowerShell-cmdlets voor implementatiesites</span><span class="sxs-lookup"><span data-stu-id="25ff1-217">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="25ff1-218">Azure PowerShell is een module die cmdlets voor het beheren van Azure via Windows PowerShell, inclusief ondersteuning voor het beheren van implementatiesites in Azure App Service biedt.</span><span class="sxs-lookup"><span data-stu-id="25ff1-218">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="25ff1-219">Zie voor informatie over het installeren en configureren van Azure PowerShell, en Azure PowerShell verifiëren met uw Azure-abonnement, [installeren en configureren van Microsoft Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="25ff1-219">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How to install and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="25ff1-220">Een webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="25ff1-220">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="25ff1-221">Een implementatiesleuf te maken</span><span class="sxs-lookup"><span data-stu-id="25ff1-221">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-to-source-slot"></a><span data-ttu-id="25ff1-222">Start een wisseling met revisie (meerdere fase swap) en doel-siteconfiguratie van toepassing op de bronsite</span><span class="sxs-lookup"><span data-stu-id="25ff1-222">Initiate a swap with review (multi-phase swap) and apply destination slot configuration to source slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="25ff1-223">Annuleren van een wisseling in behandeling (swap met revisie) en bron siteconfiguratie herstellen</span><span class="sxs-lookup"><span data-stu-id="25ff1-223">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="25ff1-224">Wisselen implementatiesites</span><span class="sxs-lookup"><span data-stu-id="25ff1-224">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="25ff1-225">Implementatiesite verwijderen</span><span class="sxs-lookup"><span data-stu-id="25ff1-225">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="25ff1-226">Azure Command-Line Interface (Azure CLI)-opdrachten voor Implementatiesites</span><span class="sxs-lookup"><span data-stu-id="25ff1-226">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="25ff1-227">De Azure CLI biedt platformoverschrijdende-opdrachten voor het werken met Azure, met inbegrip van ondersteuning voor het beheren van App Service-implementatiesites.</span><span class="sxs-lookup"><span data-stu-id="25ff1-227">The Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="25ff1-228">Zie voor instructies over het installeren en configureren van de Azure CLI, waaronder informatie over verbinding maken tussen Azure CLI en uw Azure-abonnement [installeren en configureren van de Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="25ff1-228">For instructions on installing and configuring the Azure CLI, including information on how to connect Azure CLI to your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="25ff1-229">Als u de opdrachten die beschikbaar zijn voor Azure App Service in de Azure CLI, roepen `azure site -h`.</span><span class="sxs-lookup"><span data-stu-id="25ff1-229">To list the commands available for Azure App Service in the Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="25ff1-230">Voor [Azure CLI 2.0](https://github.com/Azure/azure-cli) -opdrachten voor implementatiesites, Zie [az appservice web implementatiesleuf](/cli/azure/appservice/web/deployment/slot).</span><span class="sxs-lookup"><span data-stu-id="25ff1-230">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="25ff1-231">sitelijst voor Azure</span><span class="sxs-lookup"><span data-stu-id="25ff1-231">azure site list</span></span>
<span data-ttu-id="25ff1-232">Bel voor informatie over de apps in het huidige abonnement **azure sitelijst**, zoals in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="25ff1-232">For information about the apps in the current subscription, call **azure site list**, as in the following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="25ff1-233">Azure site maken</span><span class="sxs-lookup"><span data-stu-id="25ff1-233">azure site create</span></span>
<span data-ttu-id="25ff1-234">Aanroepen voor het maken van een implementatiesleuf **azure site maken** en geef de naam van een bestaande app en de naam van de site te maken, zoals in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="25ff1-234">To create a deployment slot, call **azure site create** and specify the name of an existing app and the name of the slot to create, as in the following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="25ff1-235">Om in te schakelen broncodebeheer voor de nieuwe site, gebruiken de **--git** optie, zoals in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="25ff1-235">To enable source control for the new slot, use the **--git** option, as in the following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="25ff1-236">Azure site wisselen</span><span class="sxs-lookup"><span data-stu-id="25ff1-236">azure site swap</span></span>
<span data-ttu-id="25ff1-237">Als u de bijgewerkte implementatie sleuf de productie-app, gebruikt u de **azure site wisselen** opdracht voor het uitvoeren van een wisselbewerking wordt uitgevoerd, zoals in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="25ff1-237">To make the updated deployment slot the production app, use the **azure site swap** command to perform a swap operation, as in the following example.</span></span> <span data-ttu-id="25ff1-238">De productie-app wordt niet uitvaltijd ondervinden, noch wordt een koude start ondergaan.</span><span class="sxs-lookup"><span data-stu-id="25ff1-238">The production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="25ff1-239">Azure site verwijderen</span><span class="sxs-lookup"><span data-stu-id="25ff1-239">azure site delete</span></span>
<span data-ttu-id="25ff1-240">Als u wilt verwijderen een implementatiesleuf die niet langer nodig is, gebruikt u de **azure site verwijderen** opdracht, zoals in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="25ff1-240">To delete a deployment slot that is no longer needed, use the **azure site delete** command, as in the following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="25ff1-241">Bekijk een web-app in werking.</span><span class="sxs-lookup"><span data-stu-id="25ff1-241">See a web app in action.</span></span> <span data-ttu-id="25ff1-242">[App Service uitproberen](https://azure.microsoft.com/try/app-service/) onmiddellijk en maak een tijdelijke app: geen creditcard nodig en zonder verdere verplichtingen.</span><span class="sxs-lookup"><span data-stu-id="25ff1-242">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="25ff1-243">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="25ff1-243">Next Steps</span></span>
<span data-ttu-id="25ff1-244">[Azure App Service-Web App – blok webtoegang tot niet-productieve implementatiesites](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Inleiding tot App-Service op Linux](./app-service-linux-intro.md)
[gratis proefversie van Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="25ff1-244">[Azure App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction to App Service on Linux](./app-service-linux-intro.md)
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

