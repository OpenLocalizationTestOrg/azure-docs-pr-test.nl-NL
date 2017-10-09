---
title: aaaAdd een CDN tooan Azure App Service | Microsoft Docs
description: Voeg een Content Delivery Network (CDN) tooan Azure App Service-toocache en leveren van de statische bestanden van servers sluiten tooyour klanten Hallo wereld.
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a><span data-ttu-id="ead1c-103">Toevoegen van een Content Delivery Network (CDN) tooan Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ead1c-103">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>

<span data-ttu-id="ead1c-104">[Azure inhoud Delivery Network (CDN)](../cdn/cdn-overview.md) statische webinhoud op strategisch geplaatste locaties tooprovide maximale doorvoer voor het leveren van inhoud toousers plaatst.</span><span class="sxs-lookup"><span data-stu-id="ead1c-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations tooprovide maximum throughput for delivering content toousers.</span></span> <span data-ttu-id="ead1c-105">Hallo CDN verlaagt ook de belasting van de server op uw web-app.</span><span class="sxs-lookup"><span data-stu-id="ead1c-105">hello CDN also decreases server load on your web app.</span></span> <span data-ttu-id="ead1c-106">Deze zelfstudie laat zien hoe tooadd Azure CDN tooa [web-app in Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ead1c-106">This tutorial shows how tooadd Azure CDN tooa [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="ead1c-107">Hier volgt Hallo introductiepagina van Hallo voorbeeld statische HTML-site waarin u met werkt:</span><span class="sxs-lookup"><span data-stu-id="ead1c-107">Here's hello home page of hello sample static HTML site that you'll work with:</span></span>

![Startpagina van voorbeeld-app](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="ead1c-109">Wat u leert het volgende:</span><span class="sxs-lookup"><span data-stu-id="ead1c-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ead1c-110">Een CDN-eindpunt maken.</span><span class="sxs-lookup"><span data-stu-id="ead1c-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="ead1c-111">Assets in cache vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="ead1c-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="ead1c-112">Gebruik query tekenreeksen in de cache opgeslagen toocontrol versies.</span><span class="sxs-lookup"><span data-stu-id="ead1c-112">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="ead1c-113">Gebruik een aangepast domein voor Hallo CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="ead1c-113">Use a custom domain for hello CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ead1c-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ead1c-114">Prerequisites</span></span>

<span data-ttu-id="ead1c-115">toocomplete in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="ead1c-115">toocomplete this tutorial:</span></span>

- [<span data-ttu-id="ead1c-116">Git installeren</span><span class="sxs-lookup"><span data-stu-id="ead1c-116">Install Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="ead1c-117">Installeer Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ead1c-117">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a><span data-ttu-id="ead1c-118">Hallo-web-app maken</span><span class="sxs-lookup"><span data-stu-id="ead1c-118">Create hello web app</span></span>

<span data-ttu-id="ead1c-119">toocreate hello web-app die u met Volg Hallo werkt [statische HTML-Quick Start](app-service-web-get-started-html.md) via Hallo **bladeren toohello app** stap.</span><span class="sxs-lookup"><span data-stu-id="ead1c-119">toocreate hello web app that you'll work with, follow hello [static HTML quickstart](app-service-web-get-started-html.md) through hello **Browse toohello app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="ead1c-120">Houd een aangepast domein bij de hand</span><span class="sxs-lookup"><span data-stu-id="ead1c-120">Have a custom domain ready</span></span>

<span data-ttu-id="ead1c-121">toocomplete hello aangepast domein stap van deze zelfstudie, u moet een aangepast domein tooown en hebben toegang tot tooyour DNS-register voor uw domeinprovider (zoals GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="ead1c-121">toocomplete hello custom domain step of this tutorial, you need tooown a custom domain and have access tooyour DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="ead1c-122">Bijvoorbeeld: tooadd DNS-vermeldingen voor `contoso.com` en `www.contoso.com`, hebt u toegang tooconfigure Hallo DNS-instellingen voor Hallo `contoso.com` hoofddomein.</span><span class="sxs-lookup"><span data-stu-id="ead1c-122">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must have access tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

<span data-ttu-id="ead1c-123">Als u nog een domeinnaam hebt, kunt u na Hallo [App Service domein zelfstudie](custom-dns-web-site-buydomains-web-app.md) toopurchase een domein met hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ead1c-123">If you don't already have a domain name, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="ead1c-124">Meld u bij toohello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="ead1c-124">Log in toohello Azure portal</span></span>

<span data-ttu-id="ead1c-125">Open een browser en ga toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ead1c-125">Open a browser and navigate toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="ead1c-126">Een CDN-profiel en -eindpunt maken</span><span class="sxs-lookup"><span data-stu-id="ead1c-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="ead1c-127">Selecteer in de Hallo linkernavigatiebalk, **App Services**, en selecteer vervolgens Hallo-app die u hebt gemaakt in Hallo [statische Quick Start voor HTML-](app-service-web-get-started-html.md).</span><span class="sxs-lookup"><span data-stu-id="ead1c-127">In hello left navigation, select **App Services**, and then select hello app that you created in hello [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![App Service-app in de Hallo portal selecteren](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="ead1c-129">In Hallo **App Service** pagina in Hallo **instellingen** sectie **Networking > Azure CDN configureren voor uw app**.</span><span class="sxs-lookup"><span data-stu-id="ead1c-129">In hello **App Service** page, in hello **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![CDN in de Hallo portal selecteren](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="ead1c-131">In Hallo **Azure Content Delivery Network** pagina, bieden Hallo **nieuw eindpunt** instellingen zoals opgegeven in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="ead1c-131">In hello **Azure Content Delivery Network** page, provide hello **New endpoint** settings as specified in hello table.</span></span>

![Profiel en -eindpunt maken in Hallo-portal](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="ead1c-133">Instelling</span><span class="sxs-lookup"><span data-stu-id="ead1c-133">Setting</span></span> | <span data-ttu-id="ead1c-134">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="ead1c-134">Suggested value</span></span> | <span data-ttu-id="ead1c-135">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ead1c-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="ead1c-136">**CDN-profiel**</span><span class="sxs-lookup"><span data-stu-id="ead1c-136">**CDN profile**</span></span> | <span data-ttu-id="ead1c-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="ead1c-137">myCDNProfile</span></span> | <span data-ttu-id="ead1c-138">Selecteer **nieuw** toocreate een CDN-profiel.</span><span class="sxs-lookup"><span data-stu-id="ead1c-138">Select **Create new** toocreate a CDN profile.</span></span> <span data-ttu-id="ead1c-139">Een CDN-profiel is een verzameling van CDN-eindpunten met Hallo dezelfde prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="ead1c-139">A CDN profile is a collection of CDN endpoints with hello same pricing tier.</span></span> |
| <span data-ttu-id="ead1c-140">**Prijscategorie**</span><span class="sxs-lookup"><span data-stu-id="ead1c-140">**Pricing tier**</span></span> | <span data-ttu-id="ead1c-141">Standard Akamai</span><span class="sxs-lookup"><span data-stu-id="ead1c-141">Standard Akamai</span></span> | <span data-ttu-id="ead1c-142">Hallo [prijscategorie](../cdn/cdn-overview.md#azure-cdn-features) Hallo-provider en de beschikbare functies.</span><span class="sxs-lookup"><span data-stu-id="ead1c-142">hello [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies hello provider and available features.</span></span> <span data-ttu-id="ead1c-143">In deze zelfstudie gebruiken we standaard Akamai.</span><span class="sxs-lookup"><span data-stu-id="ead1c-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="ead1c-144">**Naam van CDN-eindpunt**</span><span class="sxs-lookup"><span data-stu-id="ead1c-144">**CDN endpoint name**</span></span> | <span data-ttu-id="ead1c-145">De naam die uniek is in Hallo azureedge.net domein</span><span class="sxs-lookup"><span data-stu-id="ead1c-145">Any name that is unique in hello azureedge.net domain</span></span> | <span data-ttu-id="ead1c-146">U toegang tot uw resources in de cache op Hallo domein  *\<endpointname >. azureedge.net*.</span><span class="sxs-lookup"><span data-stu-id="ead1c-146">You access your cached resources at hello domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="ead1c-147">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="ead1c-147">Select **Create**.</span></span>

<span data-ttu-id="ead1c-148">Azure maakt Hallo-profiel en -eindpunt.</span><span class="sxs-lookup"><span data-stu-id="ead1c-148">Azure creates hello profile and endpoint.</span></span> <span data-ttu-id="ead1c-149">Nieuw Hallo-eindpunt wordt weergegeven in Hallo **eindpunten** lijst op dezelfde pagina Hallo en wanneer deze ingericht Hallo status **met**.</span><span class="sxs-lookup"><span data-stu-id="ead1c-149">hello new endpoint appears in hello **Endpoints** list on hello same page, and when it's provisioned hello status is **Running**.</span></span>

![Nieuw eindpunt in lijst](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="ead1c-151">Test Hallo CDN-eindpunt</span><span class="sxs-lookup"><span data-stu-id="ead1c-151">Test hello CDN endpoint</span></span>

<span data-ttu-id="ead1c-152">Als u de prijscategorie Verizon hebt geselecteerd, duurt het doorgaans ongeveer 90 minuten voor het eindpunt is ingericht.</span><span class="sxs-lookup"><span data-stu-id="ead1c-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="ead1c-153">In Akamai duurt het inrichten enkele minuten</span><span class="sxs-lookup"><span data-stu-id="ead1c-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="ead1c-154">Hallo voorbeeld-app heeft een `index.html` bestand en *css*, *img*, en *js* mappen die andere statische elementen bevatten.</span><span class="sxs-lookup"><span data-stu-id="ead1c-154">hello sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="ead1c-155">Hallo inhoud paden voor al deze bestanden zijn Hallo dezelfde op Hallo CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="ead1c-155">hello content paths for all of these files are hello same at hello CDN endpoint.</span></span> <span data-ttu-id="ead1c-156">Bijvoorbeeld, zowel van de volgende URL's Hallo Hallo toegang *bootstrap.css* bestand in Hallo *css* map:</span><span class="sxs-lookup"><span data-stu-id="ead1c-156">For example, both of hello following URLs access hello *bootstrap.css* file in hello *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="ead1c-157">Navigeer in een browser toohello volgende URL:</span><span class="sxs-lookup"><span data-stu-id="ead1c-157">Navigate a browser toohello following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![Startpagina van voorbeeldapp waarvoor de gegevens vanuit CDN worden geleverd](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="ead1c-159">U ziet Hallo dezelfde pagina dat u eerder in een Azure-web-app hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ead1c-159">You see hello same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="ead1c-160">Azure CDN activa Hallo oorsprong van web-app is opgehaald en wordt behoeve van Hallo CDN-eindpunt</span><span class="sxs-lookup"><span data-stu-id="ead1c-160">Azure CDN has retrieved hello origin web app's assets and is serving them from hello CDN endpoint</span></span>

<span data-ttu-id="ead1c-161">tooensure dat deze pagina in het Hallo CDN, vernieuwen Hallo pagina is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ead1c-161">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> <span data-ttu-id="ead1c-162">Twee aanvragen voor hello dezelfde asset soms nodig zijn om hello CDN toocache Hallo aangevraagde inhoud.</span><span class="sxs-lookup"><span data-stu-id="ead1c-162">Two requests for hello same asset are sometimes required for hello CDN toocache hello requested content.</span></span>

<span data-ttu-id="ead1c-163">Zie voor meer informatie over het maken van Azure CDN-profielen en -eindpunten [Aan de slag met Azure CDN](../cdn/cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="ead1c-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-hello-cdn"></a><span data-ttu-id="ead1c-164">Hallo CDN opschonen</span><span class="sxs-lookup"><span data-stu-id="ead1c-164">Purge hello CDN</span></span>

<span data-ttu-id="ead1c-165">Hallo CDN worden regelmatig vernieuwd daarbij behorende bronnen uit Hallo oorsprong web-app op basis van Hallo time to live (TTL)-configuratie.</span><span class="sxs-lookup"><span data-stu-id="ead1c-165">hello CDN periodically refreshes its resources from hello origin web app based on hello time-to-live (TTL) configuration.</span></span> <span data-ttu-id="ead1c-166">Hallo standaard TTL-waarde is zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="ead1c-166">hello default TTL is seven days.</span></span>

<span data-ttu-id="ead1c-167">Soms moet u mogelijk toorefresh Hallo CDN voordat Hallo verlopen van TTL--bijvoorbeeld, wanneer u de bijgewerkte inhoud toohello web-app implementeert.</span><span class="sxs-lookup"><span data-stu-id="ead1c-167">At times you might need toorefresh hello CDN before hello TTL expiration -- for example, when you deploy updated content toohello web app.</span></span> <span data-ttu-id="ead1c-168">tootrigger vernieuwen, kunt u handmatig Hallo CDN resources opschonen.</span><span class="sxs-lookup"><span data-stu-id="ead1c-168">tootrigger a refresh, you can manually purge hello CDN resources.</span></span> 

<span data-ttu-id="ead1c-169">In deze sectie van de zelfstudie hello, een wijziging toohello web-app implementeren en opschonen Hallo CDN tootrigger Hallo CDN toorefresh de cache.</span><span class="sxs-lookup"><span data-stu-id="ead1c-169">In this section of hello tutorial, you deploy a change toohello web app and purge hello CDN tootrigger hello CDN toorefresh its cache.</span></span>

### <a name="deploy-a-change-toohello-web-app"></a><span data-ttu-id="ead1c-170">Een wijziging toohello web-app implementeren</span><span class="sxs-lookup"><span data-stu-id="ead1c-170">Deploy a change toohello web app</span></span>

<span data-ttu-id="ead1c-171">Open Hallo `index.html` bestand en voeg toe '-V2 ' toohello H1-kop, zoals wordt weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="ead1c-171">Open hello `index.html` file and add "- V2" toohello H1 heading, as shown in hello following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="ead1c-172">Uw wijziging doorvoeren en het toohello web-app implementeren.</span><span class="sxs-lookup"><span data-stu-id="ead1c-172">Commit your change and deploy it toohello web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="ead1c-173">Zodra de implementatie is voltooid, Zie bladeren toohello web-app-URL en u Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ead1c-173">Once deployment has completed, browse toohello web app URL and you see hello change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

![V2 in de titel van de web-app](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="ead1c-175">Blader toohello CDN-eindpunt-URL voor het Hallo-startpagina en u niet ziet Hallo wijzigen, omdat in de cache opgeslagen versie van de Hallo in Hallo CDN nog niet is verlopen.</span><span class="sxs-lookup"><span data-stu-id="ead1c-175">Browse toohello CDN endpoint URL for hello home page and you don't see hello change because hello cached version in hello CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![Geen V2 in de titel van het CDN](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a><span data-ttu-id="ead1c-177">Hallo CDN in de portal Hallo opschonen</span><span class="sxs-lookup"><span data-stu-id="ead1c-177">Purge hello CDN in hello portal</span></span>

<span data-ttu-id="ead1c-178">tootrigger Hallo CDN tooupdate de versie van de cache, Hallo CDN opschonen.</span><span class="sxs-lookup"><span data-stu-id="ead1c-178">tootrigger hello CDN tooupdate its cached version, purge hello CDN.</span></span>

<span data-ttu-id="ead1c-179">Selecteer in de Hallo portal linkernavigatievenster, **resourcegroepen**, en selecteer vervolgens Hallo resourcegroep die u hebt gemaakt voor uw web-app (myResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="ead1c-179">In hello portal left navigation, select **Resource groups**, and then select hello resource group that you created for your web app (myResourceGroup).</span></span>

![Resourcegroep selecteren](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="ead1c-181">Selecteer in de lijst met resources Hallo uw CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="ead1c-181">In hello list of resources, select your CDN endpoint.</span></span>

![Eindpunt selecteren](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="ead1c-183">Hallo boven aan het Hallo **eindpunt** pagina, klikt u op **opschonen**.</span><span class="sxs-lookup"><span data-stu-id="ead1c-183">At hello top of hello **Endpoint** page, click **Purge**.</span></span>

![Leegmaken selecteren](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="ead1c-185">Voer Hallo paden naar inhoud gewenste toopurge.</span><span class="sxs-lookup"><span data-stu-id="ead1c-185">Enter hello content paths you wish toopurge.</span></span> <span data-ttu-id="ead1c-186">U kunt een volledig bestand pad toopurge geeft een afzonderlijk bestand of een segment pad toopurge en Vernieuw alle inhoud in een map.</span><span class="sxs-lookup"><span data-stu-id="ead1c-186">You can pass a complete file path toopurge an individual file, or a path segment toopurge and refresh all content in a folder.</span></span> <span data-ttu-id="ead1c-187">Omdat u gewijzigd `index.html`, zorg ervoor dat deze een van de paden Hallo.</span><span class="sxs-lookup"><span data-stu-id="ead1c-187">Since you changed `index.html`, make sure that is one of hello paths.</span></span>

<span data-ttu-id="ead1c-188">Selecteer onderaan Hallo Hallo pagina, **opschonen**.</span><span class="sxs-lookup"><span data-stu-id="ead1c-188">At hello bottom of hello page, select **Purge**.</span></span>

![Pagina leegmaken](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a><span data-ttu-id="ead1c-190">Controleer of deze Hallo die CDN is bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="ead1c-190">Verify that hello CDN is updated</span></span>

<span data-ttu-id="ead1c-191">Wacht totdat de Hallo opschonen aanvraag is verwerkt, doorgaans een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="ead1c-191">Wait until hello purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="ead1c-192">toosee hello huidige status, selecteer Hallo belpictogram bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="ead1c-192">toosee hello current status, select hello bell icon at hello top of hello page.</span></span> 

![Melding voor leegmaken](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="ead1c-194">Blader toohello CDN-eindpunt-URL voor `index.html`, en u ziet nu Hallo V2 dat u op de startpagina Hallo toohello titel toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ead1c-194">Browse toohello CDN endpoint URL for `index.html`, and now you see hello V2 that you added toohello title on hello home page.</span></span> <span data-ttu-id="ead1c-195">Dit betekent dat Hallo CDN cache is vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="ead1c-195">This shows that hello CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![V2 in de titel van het CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="ead1c-197">Zie voor meer informatie [Een Azure CDN-eindpunt leegmaken](../cdn/cdn-purge-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="ead1c-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-tooversion-content"></a><span data-ttu-id="ead1c-198">Query tekenreeksen tooversion inhoud gebruiken</span><span class="sxs-lookup"><span data-stu-id="ead1c-198">Use query strings tooversion content</span></span>

<span data-ttu-id="ead1c-199">Hello Azure CDN biedt Hallo cacheopties gedrag te volgen:</span><span class="sxs-lookup"><span data-stu-id="ead1c-199">hello Azure CDN offers hello following caching behavior options:</span></span>

* <span data-ttu-id="ead1c-200">Queryreeksen negeren</span><span class="sxs-lookup"><span data-stu-id="ead1c-200">Ignore query strings</span></span>
* <span data-ttu-id="ead1c-201">Queryreeksen in de cache opslaan overslaan</span><span class="sxs-lookup"><span data-stu-id="ead1c-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="ead1c-202">Elke unieke URL in de cache opslaan</span><span class="sxs-lookup"><span data-stu-id="ead1c-202">Cache every unique URL</span></span> 

<span data-ttu-id="ead1c-203">Hallo eerst van deze is standaard hello, wat betekent dat er slechts één versie van een asset ongeacht Hallo queryreeks in Hallo URL-cache.</span><span class="sxs-lookup"><span data-stu-id="ead1c-203">hello first of these is hello default, which means there is only one cached version of an asset regardless of hello query string in hello URL.</span></span> 

<span data-ttu-id="ead1c-204">In deze sectie van de zelfstudie Hallo wijzigen u opslaan in cache gedrag toocache voor elke unieke URL Hallo.</span><span class="sxs-lookup"><span data-stu-id="ead1c-204">In this section of hello tutorial, you change hello caching behavior toocache every unique URL.</span></span>

### <a name="change-hello-cache-behavior"></a><span data-ttu-id="ead1c-205">Hallo cache gedrag wijzigen</span><span class="sxs-lookup"><span data-stu-id="ead1c-205">Change hello cache behavior</span></span>

<span data-ttu-id="ead1c-206">In de Azure-portal Hallo **CDN-eindpunt** pagina **Cache**.</span><span class="sxs-lookup"><span data-stu-id="ead1c-206">In hello Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="ead1c-207">Selecteer **elke unieke URL in de Cache** van Hallo **queryreeks cachegedrag** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="ead1c-207">Select **Cache every unique URL** from hello **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="ead1c-208">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ead1c-208">Select **Save**.</span></span>

![Selecteer cachegedrag van queryreeks](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="ead1c-210">Controleren of de unieke URL's afzonderlijk in de cache worden opgeslagen</span><span class="sxs-lookup"><span data-stu-id="ead1c-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="ead1c-211">In een browser navigeren toohello introductiepagina op Hallo CDN-eindpunt, maar u een querytekenreeks:</span><span class="sxs-lookup"><span data-stu-id="ead1c-211">In a browser, navigate toohello home page at hello CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="ead1c-212">Hallo CDN retourneert Hallo huidige web app-inhoud, waaronder 'V2' hello post.</span><span class="sxs-lookup"><span data-stu-id="ead1c-212">hello CDN returns hello current web app content, which includes "V2" in hello heading.</span></span> 

<span data-ttu-id="ead1c-213">tooensure dat deze pagina in het Hallo CDN, vernieuwen Hallo pagina is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ead1c-213">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> 

<span data-ttu-id="ead1c-214">Open `index.html` en wijzig 'V2' te 'V3', en implementeren van Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ead1c-214">Open `index.html` and change "V2" too"V3", and deploy hello change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="ead1c-215">Ga in een browser toohello CDN-eindpunt-URL met een nieuwe querytekenreeks, zoals `q=2`.</span><span class="sxs-lookup"><span data-stu-id="ead1c-215">In a browser, go toohello CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="ead1c-216">Hallo CDN opgehaald Hallo huidige `index.html` bestands- en 'V3' wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ead1c-216">hello CDN gets hello current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="ead1c-217">Maar als u de navigatiefunctie toohello CDN-eindpunt met Hallo `q=1` queryreeks, ziet u 'V2'.</span><span class="sxs-lookup"><span data-stu-id="ead1c-217">But if you navigate toohello CDN endpoint with hello `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![V3 in de titel in het CDN, queryreeks 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![V2 in de titel in het CDN, queryreeks 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="ead1c-220">Deze uitvoer toont elke queryreeks anders wordt behandeld:</span><span class="sxs-lookup"><span data-stu-id="ead1c-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="ead1c-221">q = 1 werd gebruikt voorafgaand aan, zodat inhoud in cache (V2) worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ead1c-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="ead1c-222">q = 2 is nieuw, dus Hallo nieuwste web app inhoud worden opgehaald en (V3) geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ead1c-222">q=2 is new, so hello latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="ead1c-223">Zie [Cachegedrag in Azure CDN bepalen met queryreeksen](../cdn/cdn-query-string.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ead1c-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a><span data-ttu-id="ead1c-224">Toewijzen van een aangepast domein tooa CDN-eindpunt</span><span class="sxs-lookup"><span data-stu-id="ead1c-224">Map a custom domain tooa CDN endpoint</span></span>

<span data-ttu-id="ead1c-225">U hebt uw aangepaste domein tooyour CDN-eindpunt toewijzen door een CNAME-record te maken.</span><span class="sxs-lookup"><span data-stu-id="ead1c-225">You'll map your custom domain tooyour CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="ead1c-226">Een CNAME-record is een DNS-functie waarmee een brondomein domein tooa bestemming.</span><span class="sxs-lookup"><span data-stu-id="ead1c-226">A CNAME record is a DNS feature that maps a source domain tooa destination domain.</span></span> <span data-ttu-id="ead1c-227">U kunt bijvoorbeeld toewijzen `cdn.contoso.com` of `static.contoso.com` te`contoso.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="ead1c-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` too`contoso.azureedge.net`.</span></span>

<span data-ttu-id="ead1c-228">Als u een aangepast domein niet hebt, kunt u na Hallo [App Service domein zelfstudie](custom-dns-web-site-buydomains-web-app.md) toopurchase een domein met hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ead1c-228">If you don't have a custom domain, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a><span data-ttu-id="ead1c-229">Hallo hostnaam toouse Hello CNAME vinden</span><span class="sxs-lookup"><span data-stu-id="ead1c-229">Find hello hostname toouse with hello CNAME</span></span>

<span data-ttu-id="ead1c-230">In Azure-portal Hallo **eindpunt** pagina, controleert u of **overzicht** is geselecteerd in de navigatie en selecteer vervolgens Hallo Hallo **+ aangepaste domeinen** knop bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="ead1c-230">In hello Azure portal **Endpoint** page, make sure **Overview** is selected in hello left navigation, and then select hello **+ Custom Domain** button at hello top of hello page.</span></span>

![Aangepast domein toevoegen selecteren](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="ead1c-232">In Hallo **toevoegen van een aangepast domein** pagina ziet u Hallo eindpunt host naam toouse bij het maken van een CNAME-record.</span><span class="sxs-lookup"><span data-stu-id="ead1c-232">In hello **Add a custom domain** page, you see hello endpoint host name toouse in creating a CNAME record.</span></span> <span data-ttu-id="ead1c-233">Hallo-hostnaam is afgeleid van uw CDN-eindpunt-URL:  **&lt;EndpointName >. azureedge.net**.</span><span class="sxs-lookup"><span data-stu-id="ead1c-233">hello host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![Een domeinpagina toevoegen](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a><span data-ttu-id="ead1c-235">Hallo CNAME configureren bij uw domeinregistrar</span><span class="sxs-lookup"><span data-stu-id="ead1c-235">Configure hello CNAME with your domain registrar</span></span>

<span data-ttu-id="ead1c-236">Navigeer tooyour domeinregistrar website en Hallo sectie voor het maken van DNS-records gevonden.</span><span class="sxs-lookup"><span data-stu-id="ead1c-236">Navigate tooyour domain registrar's web site, and locate hello section for creating DNS records.</span></span> <span data-ttu-id="ead1c-237">U vindt dit in een gedeelte zoals **Domeinnaam**, **DNS** of **Serverbeheernaam**.</span><span class="sxs-lookup"><span data-stu-id="ead1c-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="ead1c-238">Hallo sectie voor het beheren van CNAME-records vinden.</span><span class="sxs-lookup"><span data-stu-id="ead1c-238">Find hello section for managing CNAMEs.</span></span> <span data-ttu-id="ead1c-239">U kunt toogo tooan geavanceerde instellingenpagina hebben en zoekt Hallo woorden CNAME-, Alias- of subdomeinen.</span><span class="sxs-lookup"><span data-stu-id="ead1c-239">You may have toogo tooan advanced settings page and look for hello words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="ead1c-240">Een CNAME-record maken die uw gekozen subdomein toegewezen (bijvoorbeeld **statische** of **cdn**) toohello **eindpunt hostnaam** die eerder in Hallo portal weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ead1c-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) toohello **Endpoint host name** shown earlier in hello portal.</span></span> 

### <a name="enter-hello-custom-domain-in-azure"></a><span data-ttu-id="ead1c-241">Hallo aangepast domein invoeren in Azure</span><span class="sxs-lookup"><span data-stu-id="ead1c-241">Enter hello custom domain in Azure</span></span>

<span data-ttu-id="ead1c-242">Retourneren van toohello **toevoegen van een aangepast domein** pagina en voert u uw aangepaste domein, met inbegrip van subdomein hello, in het dialoogvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="ead1c-242">Return toohello **Add a custom domain** page, and enter your custom domain, including hello subdomain, in hello dialog box.</span></span> <span data-ttu-id="ead1c-243">Geef bijvoorbeeld `cdn.contoso.com` op.</span><span class="sxs-lookup"><span data-stu-id="ead1c-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="ead1c-244">Azure wordt gecontroleerd of Hallo CNAME-record bestaat voor Hallo-domeinnaam die u hebt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="ead1c-244">Azure verifies that hello CNAME record exists for hello domain name you have entered.</span></span> <span data-ttu-id="ead1c-245">Als Hallo CNAME juist is, kan uw aangepaste domein wordt gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="ead1c-245">If hello CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="ead1c-246">Voor Hallo CNAME-record toopropagate tooname servers op Hallo Internet kan tijd duren.</span><span class="sxs-lookup"><span data-stu-id="ead1c-246">It can take time for hello CNAME record toopropagate tooname servers on hello Internet.</span></span> <span data-ttu-id="ead1c-247">Als uw domein is niet onmiddellijk gevalideerd, wacht een paar minuten en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="ead1c-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-hello-custom-domain"></a><span data-ttu-id="ead1c-248">Test Hallo aangepast domein</span><span class="sxs-lookup"><span data-stu-id="ead1c-248">Test hello custom domain</span></span>

<span data-ttu-id="ead1c-249">Navigeer in een browser toohello `index.html` bestand met behulp van uw aangepaste domein (bijvoorbeeld `cdn.contoso.com/index.html`) tooverify die Hallo resultaat is hetzelfde als wanneer u gaat rechtstreeks te Hallo`<endpointname>azureedge.net/index.html`.</span><span class="sxs-lookup"><span data-stu-id="ead1c-249">In a browser, navigate toohello `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) tooverify that hello result is hello same as when you go directly too`<endpointname>azureedge.net/index.html`.</span></span>

![Startpagina van voorbeeldapp met URL van aangepast domein](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="ead1c-251">Zie voor meer informatie [kaart Azure CDN inhoud tooa aangepast domein](../cdn/cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="ead1c-251">For more information, see [Map Azure CDN content tooa custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="ead1c-252">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ead1c-252">Next steps</span></span>

<span data-ttu-id="ead1c-253">Wat u hebt geleerd:</span><span class="sxs-lookup"><span data-stu-id="ead1c-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ead1c-254">Een CDN-eindpunt maken.</span><span class="sxs-lookup"><span data-stu-id="ead1c-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="ead1c-255">Assets in cache vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="ead1c-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="ead1c-256">Gebruik query tekenreeksen in de cache opgeslagen toocontrol versies.</span><span class="sxs-lookup"><span data-stu-id="ead1c-256">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="ead1c-257">Gebruik een aangepast domein voor Hallo CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="ead1c-257">Use a custom domain for hello CDN endpoint.</span></span>

<span data-ttu-id="ead1c-258">Meer informatie over hoe toooptimize CDN prestaties in Hallo volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="ead1c-258">Learn how toooptimize CDN performance in hello following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ead1c-259">De prestaties verbeteren door bestanden in Azure CDN te comprimeren</span><span class="sxs-lookup"><span data-stu-id="ead1c-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="ead1c-260">Vooraf assets op een Azure CDN-eindpunt laden</span><span class="sxs-lookup"><span data-stu-id="ead1c-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
