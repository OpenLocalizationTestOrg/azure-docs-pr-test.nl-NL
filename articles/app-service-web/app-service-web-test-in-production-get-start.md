---
title: Aan de slag met testen tijdens productie voor Web Apps
description: Meer informatie over de Test in productie (TiP)-functie in Azure App Service Web Apps.
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 4623468d-886e-4203-8012-8f86deb2790b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: cephalin
ms.openlocfilehash: 9f38b635140cacf0513c75385bce3c110a930969
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-test-in-production-for-web-apps"></a><span data-ttu-id="f4fd9-103">Aan de slag met testen tijdens productie voor Web Apps</span><span class="sxs-lookup"><span data-stu-id="f4fd9-103">Get started with test in production for Web Apps</span></span>
<span data-ttu-id="f4fd9-104">In productie testen of live-testen van uw web-app met behulp van de live klantverkeer, is een test-strategie die app-ontwikkelaars steeds integreren in hun [flexibele ontwikkeling](https://en.wikipedia.org/wiki/Agile_software_development) methodologie.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-104">Testing in production, or live-testing your web app using live customer traffic, is a test strategy that app developers increasingly integrate into their [agile development](https://en.wikipedia.org/wiki/Agile_software_development) methodology.</span></span> <span data-ttu-id="f4fd9-105">Hiermee kunt u de kwaliteit van uw apps met live gebruikersverkeer in uw productieomgeving, in plaats van de kunstmatige gegevens in een testomgeving te testen.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-105">It enables you to test the quality of your apps with live user traffic in your production environment, as opposed to synthesized data in a test environment.</span></span> <span data-ttu-id="f4fd9-106">Bij het blootstellen van uw nieuwe app voor echte gebruikers kunt u geïnformeerd over de echte problemen die uw app hebben te maken mogelijk nadat deze is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-106">By exposing your new app to real users, you can be informed on the real problems your app may face once it is deployed.</span></span> <span data-ttu-id="f4fd9-107">U kunt controleren of de functionaliteit, de prestaties en de waarde van uw app-updates op basis van het volume, snelheid en diverse echte gebruikersverkeer, wat u nooit in een testomgeving geschatte kunt.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-107">You can verify the functionality, performance, and value of your app updates against the volume, velocity, and variety of real user traffic, which you can never approximate in a test environment.</span></span>

## <a name="traffic-routing-in-app-service-web-apps"></a><span data-ttu-id="f4fd9-108">Verkeer routering in App Service-Web-Apps</span><span class="sxs-lookup"><span data-stu-id="f4fd9-108">Traffic Routing in App Service Web Apps</span></span>
<span data-ttu-id="f4fd9-109">Met de functie voor verkeersroutering in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), u kunt instellen dat een deel van live gebruikersverkeer op een of meer [implementatiesites](web-sites-staged-publishing.md), en vervolgens uw app met analyseren [Azure-toepassing Insights](/services/application-insights/) of [Azure HDInsight](/services/hdinsight/), of een hulpprogramma van derden, zoals [New Relic](/marketplace/partners/newrelic/newrelic/) voor het valideren van de wijziging.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-109">With the Traffic Routing feature in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can direct a portion of live user traffic to one or more [deployment slots](web-sites-staged-publishing.md), and then analyze your app with [Azure Application Insights](/services/application-insights/) or [Azure HDInsight](/services/hdinsight/), or a third-party tool like [New Relic](/marketplace/partners/newrelic/newrelic/) to validate your change.</span></span> <span data-ttu-id="f4fd9-110">U kunt bijvoorbeeld de volgende scenario's implementeren met App Service:</span><span class="sxs-lookup"><span data-stu-id="f4fd9-110">For example, you can implement the following scenarios with App Service:</span></span>

* <span data-ttu-id="f4fd9-111">Functionele bugs detecteren of knelpunten in uw updates voorafgaand aan de implementatie van de gehele site speldenpunt</span><span class="sxs-lookup"><span data-stu-id="f4fd9-111">Discover functional bugs or pinpoint performance bottlenecks in your updates prior to site-wide deployment</span></span>
* <span data-ttu-id="f4fd9-112">"Gecontroleerde test vlucht' van de wijzigingen door te meten bruikbaarheid metrische gegevens over de bèta-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f4fd9-112">Perform "controlled test flights" of your changes by measuring usability metrics on the beta app</span></span>
* <span data-ttu-id="f4fd9-113">Geleidelijk mogelijk uitbreiden tot een nieuwe update en probleemloos weer omlaag naar de huidige versie als een fout optreedt</span><span class="sxs-lookup"><span data-stu-id="f4fd9-113">Gradually ramp up to a new update, and gracefully back down to the current version if an error occurs</span></span> 
* <span data-ttu-id="f4fd9-114">Optimaliseert u uw app bedrijfsresultaten door [A / B-tests](https://en.wikipedia.org/wiki/A/B_testing) of [multidimensionale tests](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) meerdere implementatiesites</span><span class="sxs-lookup"><span data-stu-id="f4fd9-114">Optimize your app's business results by running [A/B tests](https://en.wikipedia.org/wiki/A/B_testing) or [multivariate tests](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) in multiple deployment slots</span></span>

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a><span data-ttu-id="f4fd9-115">Vereisten voor het gebruik van verkeersroutering in Web-Apps</span><span class="sxs-lookup"><span data-stu-id="f4fd9-115">Requirements for using Traffic Routing in Web Apps</span></span>
* <span data-ttu-id="f4fd9-116">Uw web-app moet worden uitgevoerd in **standaard** of **Premium** laag, zoals vereist is voor meerdere implementatiesites.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-116">Your web app must run in **Standard** or **Premium** tier, as it is required for multiple deployment slots.</span></span>
* <span data-ttu-id="f4fd9-117">Een goede werking verkeersroutering cookies zijn ingeschakeld in de browser van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-117">In order to work properly, Traffic Routing requires cookies to be enabled in the users' browser.</span></span> <span data-ttu-id="f4fd9-118">Traffic Routing worden cookies gebruikt vastmaken een clientbrowser in de implementatiesleuf van een voor de levensduur van de clientsessie.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-118">Traffic Routing uses cookies to pin a client browser to a deployment slot for the life the client session.</span></span>
* <span data-ttu-id="f4fd9-119">Traffic Routing biedt ondersteuning voor geavanceerde TiP-scenario's via Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-119">Traffic Routing supports advanced TiP scenarios through Azure PowerShell cmdlets.</span></span>

## <a name="route-traffic-segment-to-a-deployment-slot"></a><span data-ttu-id="f4fd9-120">Route verkeer segment moet een implementatiesleuf</span><span class="sxs-lookup"><span data-stu-id="f4fd9-120">Route traffic segment to a deployment slot</span></span>
<span data-ttu-id="f4fd9-121">Op het niveau basis van elk scenario TiP kunt u een vooraf gedefinieerde percentage van uw live verkeer naar een niet-productieve implementatiesleuf routeren.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-121">At the basic level in every TiP scenario, you route a predefined percentage of your live traffic to a non-production deployment slot.</span></span> <span data-ttu-id="f4fd9-122">U doet dit door de volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="f4fd9-122">To do this, follow the steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="f4fd9-123">Hier de stappen wordt ervan uitgegaan dat er al een [niet-productieve implementatiesleuf](web-sites-staged-publishing.md) en dat de gewenste web-app-inhoud is al [geïmplementeerd](web-sites-deploy.md) aan.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-123">The steps here assumes that you already have a [non-production deployment slot](web-sites-staged-publishing.md) and that the desired web app content is already [deployed](web-sites-deploy.md) to it.</span></span>
> 
> 

1. <span data-ttu-id="f4fd9-124">Meld u aan bij de [Azure-Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f4fd9-124">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f4fd9-125">Klik op de blade van uw web-app **instellingen** > **verkeersroutering**.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-125">In your web app's blade, click **Settings** > **Traffic Routing**.</span></span>
   ![](./media/app-service-web-test-in-production/01-traffic-routing.png)
3. <span data-ttu-id="f4fd9-126">Selecteer de site die u wilt routeren van verkeer en het percentage van het totale verkeer u wenst op en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-126">Select the slot that you want to route traffic to and the percentage of the total traffic you desire, then click **Save**.</span></span>
   
    ![](./media/app-service-web-test-in-production/02-select-slot.png)
4. <span data-ttu-id="f4fd9-127">Ga naar de implementatiesleuf blade.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-127">Go to the deployment slot's blade.</span></span> <span data-ttu-id="f4fd9-128">U ziet nu live verkeer wordt doorgestuurd naar het.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-128">You should now see live traffic being routed to it.</span></span>
   
    ![](./media/app-service-web-test-in-production/03-traffic-routed.png)

<span data-ttu-id="f4fd9-129">Zodra voor verkeersroutering is geconfigureerd, wordt het opgegeven percentage van clients willekeurig worden gerouteerd naar uw-productiesite.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-129">Once Traffic Routing is configured, the specified percentage of clients will be randomly routed to your non-production slot.</span></span> <span data-ttu-id="f4fd9-130">Het is echter belangrijk te weten dat wanneer een client wordt automatisch doorgestuurd naar een specifieke site, deze worden '' aan die sleuf voor de levensduur van die clientsessie vastgemaakt wordt.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-130">However, it is important to note that once a client is automatically routed to a specific slot, it will be "pinned" to that slot for the life of that client session.</span></span> <span data-ttu-id="f4fd9-131">Dit gedaan met behulp van een cookie om de gebruikerssessie vast te maken.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-131">This done using a cookie to pin the user session.</span></span> <span data-ttu-id="f4fd9-132">Als u de HTTP-aanvragen inspecteren, vindt u een `TipMix` cookie in elke volgende aanvraag.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-132">If you inspect the HTTP requests, you will find a `TipMix` cookie in every subsequent request.</span></span>

![](./media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-to-a-specific-slot"></a><span data-ttu-id="f4fd9-133">Clientaanvragen omzetten in een specifieke site</span><span class="sxs-lookup"><span data-stu-id="f4fd9-133">Force client requests to a specific slot</span></span>
<span data-ttu-id="f4fd9-134">Naast de automatische verkeersroutering kan App Service route-aanvragen voor een specifieke site.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-134">In addition to automatic traffic routing, App Service is able to route requests to a specific slot.</span></span> <span data-ttu-id="f4fd9-135">Dit is handig als u wilt dat gebruikers kunnen kiezen in of opt-out van uw app beta.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-135">This is useful when you want your users to be able to opt-into or opt-out of your beta app.</span></span> <span data-ttu-id="f4fd9-136">Hiervoor gebruikt u de `x-ms-routing-name` queryparameter.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-136">To do this, you use the `x-ms-routing-name` query parameter.</span></span>

<span data-ttu-id="f4fd9-137">Gebruikers in een specifieke sleuf met omgeleid `x-ms-routing-name`, moet u ervoor zorgen dat de sleuf is al toegevoegd aan de lijst voor verkeersroutering.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-137">To reroute users to a specific slot using `x-ms-routing-name`, you must make sure that the slot is already added to the Traffic Routing list.</span></span> <span data-ttu-id="f4fd9-138">Omdat u routeren expliciet naar een site wilt, worden de werkelijke routering u percentage ingesteld maakt niet uit.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-138">Since you want to route to a slot explicitly, the actual routing percentage you set doesn't matter.</span></span> <span data-ttu-id="f4fd9-139">Als u wilt, kunt u een 'beta koppeling' waarop gebruikers klikken kunnen om toegang tot de app beta opgesteld.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-139">If you want, you can craft a "beta link" that users can click to access the beta app.</span></span>

![](./media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a><span data-ttu-id="f4fd9-140">Gebruikers buiten de bèta-app kiezen</span><span class="sxs-lookup"><span data-stu-id="f4fd9-140">Opt users out of beta app</span></span>
<span data-ttu-id="f4fd9-141">Zodat gebruikers afmelden uw bèta-app kunt u bijvoorbeeld deze koppeling in uw webpagina plaatsen:</span><span class="sxs-lookup"><span data-stu-id="f4fd9-141">To let users opt out of your beta app, for example, you can put this link in your web page:</span></span>

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back to production app</a>

<span data-ttu-id="f4fd9-142">De tekenreeks `x-ms-routing-name=self` Hiermee geeft u de productiesite.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-142">The string `x-ms-routing-name=self` specifies the production slot.</span></span> <span data-ttu-id="f4fd9-143">Zodra de clientbrowser toegang krijgen tot de koppeling, niet alleen het omgeleid naar de productiesite, maar elke volgende aanvraag bevat de `x-ms-routing-name=self` cookie die pincodes van de sessie naar de productiesite.</span><span class="sxs-lookup"><span data-stu-id="f4fd9-143">Once the client browser access the link, not only is it redirected to the production slot, but every subsequent request will contain the `x-ms-routing-name=self` cookie that pins the session to the production slot.</span></span>

![](./media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-to-beta-app"></a><span data-ttu-id="f4fd9-144">Gebruikers in beta app kiezen</span><span class="sxs-lookup"><span data-stu-id="f4fd9-144">Opt users in to beta app</span></span>
<span data-ttu-id="f4fd9-145">Om gebruikers te laten deelnemen aan uw app beta, stelt u de dezelfde queryparameter bijvoorbeeld op de naam van de niet-productiesite:</span><span class="sxs-lookup"><span data-stu-id="f4fd9-145">To let users opt in to your beta app, set the same query parameter to the name of the non-production slot, for example:</span></span>

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a><span data-ttu-id="f4fd9-146">Meer bronnen</span><span class="sxs-lookup"><span data-stu-id="f4fd9-146">More resources</span></span>
* [<span data-ttu-id="f4fd9-147">Faseringsomgevingen voor web-apps in Azure App Service instellen</span><span class="sxs-lookup"><span data-stu-id="f4fd9-147">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)
* [<span data-ttu-id="f4fd9-148">Een complexe toepassing zoals verwacht in Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="f4fd9-148">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="f4fd9-149">Flexibele software ontwikkelen met Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f4fd9-149">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)
* [<span data-ttu-id="f4fd9-150">DevOps-omgevingen effectief gebruiken voor uw web-apps</span><span class="sxs-lookup"><span data-stu-id="f4fd9-150">Use DevOps environments effectively for your web apps</span></span>](app-service-web-staged-publishing-realworld-scenarios.md)

