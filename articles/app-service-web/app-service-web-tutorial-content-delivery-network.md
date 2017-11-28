---
title: Een CDN toevoegen aan een Azure App Service | Microsoft Docs
description: Voeg een netwerk voor contentlevering toe aan een Azure App Service, zodat uw statische bestanden altijd worden gecached en geleverd vanaf een server dicht bij uw klanten, overal ter wereld.
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 257b75d01f3904661c1a188a2d53ffcb74f48f06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-content-delivery-network-cdn-to-an-azure-app-service"></a><span data-ttu-id="f4b5c-103">Een netwerk voor contentlevering toevoegen aan een Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f4b5c-103">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>

<span data-ttu-id="f4b5c-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) slaat op strategisch geplaatste locaties statische webinhoud in de cache op om een maximale doorvoer voor de levering van inhoud te waarborgen.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations to provide maximum throughput for delivering content to users.</span></span> <span data-ttu-id="f4b5c-105">De CDN vermindert ook de serverbelasting van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-105">The CDN also decreases server load on your web app.</span></span> <span data-ttu-id="f4b5c-106">In deze zelfstudie leest u hoe u Azure CDN toevoegt aan een [web-app in de Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4b5c-106">This tutorial shows how to add Azure CDN to a [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="f4b5c-107">Dit is de startpagina van de statische HTML-voorbeeldsite die u gaat gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f4b5c-107">Here's the home page of the sample static HTML site that you'll work with:</span></span>

![Startpagina van voorbeeld-app](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="f4b5c-109">Wat u leert het volgende:</span><span class="sxs-lookup"><span data-stu-id="f4b5c-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f4b5c-110">Een CDN-eindpunt maken.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="f4b5c-111">Assets in cache vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="f4b5c-112">Queryreeksen gebruiken voor het beheren van versies in cache.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-112">Use query strings to control cached versions.</span></span>
> * <span data-ttu-id="f4b5c-113">Een aangepast domein gebruiken voor het CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-113">Use a custom domain for the CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4b5c-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f4b5c-114">Prerequisites</span></span>

<span data-ttu-id="f4b5c-115">Vereisten voor het voltooien van deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="f4b5c-115">To complete this tutorial:</span></span>

- [<span data-ttu-id="f4b5c-116">Git installeren</span><span class="sxs-lookup"><span data-stu-id="f4b5c-116">Install Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="f4b5c-117">Installeer Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f4b5c-117">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-the-web-app"></a><span data-ttu-id="f4b5c-118">De web-app maken</span><span class="sxs-lookup"><span data-stu-id="f4b5c-118">Create the web app</span></span>

<span data-ttu-id="f4b5c-119">Volg voor het maken van de web-app u met werkt de [statische HTML-Quick Start](app-service-web-get-started-html.md) via de **Blader naar de app** stap.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-119">To create the web app that you'll work with, follow the [static HTML quickstart](app-service-web-get-started-html.md) through the **Browse to the app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="f4b5c-120">Houd een aangepast domein bij de hand</span><span class="sxs-lookup"><span data-stu-id="f4b5c-120">Have a custom domain ready</span></span>

<span data-ttu-id="f4b5c-121">Als u wilt de stap van het aangepaste domein van deze zelfstudie hebt voltooid, moet u eigenaar bent van een aangepast domein en toegang hebben tot uw DNS-register voor uw domeinprovider (zoals GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="f4b5c-121">To complete the custom domain step of this tutorial, you need to own a custom domain and have access to your DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="f4b5c-122">Als u bijvoorbeeld DNS-vermeldingen voor `contoso.com` en `www.contoso.com` wilt toevoegen, moet u de DNS-instellingen voor het hoofddomein van `contoso.com` kunnen configureren.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-122">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must have access to configure the DNS settings for the `contoso.com` root domain.</span></span>

<span data-ttu-id="f4b5c-123">Als u nog geen domeinnaam hebt, overweeg dan de [Zelfstudie over App Service-domeinen](custom-dns-web-site-buydomains-web-app.md) te volgen om een domein aan te schaffen met de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-123">If you don't already have a domain name, consider following the [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) to purchase a domain using the Azure portal.</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="f4b5c-124">Aanmelden bij Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f4b5c-124">Log in to the Azure portal</span></span>

<span data-ttu-id="f4b5c-125">Open een browser en navigeer naar de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f4b5c-125">Open a browser and navigate to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="f4b5c-126">Een CDN-profiel en -eindpunt maken</span><span class="sxs-lookup"><span data-stu-id="f4b5c-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="f4b5c-127">Selecteer in het navigatiedeelvenster links **App Services** en selecteer vervolgens de app die u hebt gemaakt in de [Quickstart voor statische HTML](app-service-web-get-started-html.md).</span><span class="sxs-lookup"><span data-stu-id="f4b5c-127">In the left navigation, select **App Services**, and then select the app that you created in the [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![Een App Service-app in de portal selecteren](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="f4b5c-129">Selecteer op de pagina **App Service** in het gedeelte **Instellingen** de optie **Netwerken > Azure CDN configureren voor uw app**.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-129">In the **App Service** page, in the **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![CDN selecteren in de portal](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="f4b5c-131">Geef op de pagina **Azure Content Delivery Network** de instellingen voor **Nieuw eindpunt** op zoals aangegeven in de tabel.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-131">In the **Azure Content Delivery Network** page, provide the **New endpoint** settings as specified in the table.</span></span>

![Een profiel en eindpunt maken in de portal](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="f4b5c-133">Instelling</span><span class="sxs-lookup"><span data-stu-id="f4b5c-133">Setting</span></span> | <span data-ttu-id="f4b5c-134">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="f4b5c-134">Suggested value</span></span> | <span data-ttu-id="f4b5c-135">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f4b5c-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="f4b5c-136">**CDN-profiel**</span><span class="sxs-lookup"><span data-stu-id="f4b5c-136">**CDN profile**</span></span> | <span data-ttu-id="f4b5c-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="f4b5c-137">myCDNProfile</span></span> | <span data-ttu-id="f4b5c-138">Selecteer **nieuw** een CDN-profiel maken.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-138">Select **Create new** to create a CDN profile.</span></span> <span data-ttu-id="f4b5c-139">Een CDN-profiel is een verzameling van CDN-eindpunten van dezelfde prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-139">A CDN profile is a collection of CDN endpoints with the same pricing tier.</span></span> |
| <span data-ttu-id="f4b5c-140">**Prijscategorie**</span><span class="sxs-lookup"><span data-stu-id="f4b5c-140">**Pricing tier**</span></span> | <span data-ttu-id="f4b5c-141">Standard Akamai</span><span class="sxs-lookup"><span data-stu-id="f4b5c-141">Standard Akamai</span></span> | <span data-ttu-id="f4b5c-142">De [prijscategorie](../cdn/cdn-overview.md#azure-cdn-features) geeft de provider en de beschikbare functies aan.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-142">The [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies the provider and available features.</span></span> <span data-ttu-id="f4b5c-143">In deze zelfstudie gebruiken we standaard Akamai.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="f4b5c-144">**Naam van CDN-eindpunt**</span><span class="sxs-lookup"><span data-stu-id="f4b5c-144">**CDN endpoint name**</span></span> | <span data-ttu-id="f4b5c-145">Een unieke naam in het domein azureedge.net</span><span class="sxs-lookup"><span data-stu-id="f4b5c-145">Any name that is unique in the azureedge.net domain</span></span> | <span data-ttu-id="f4b5c-146">U heeft toegang tot uw resources in de cache via het domein  *\<endpointname>.azureedge.net*.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-146">You access your cached resources at the domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="f4b5c-147">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-147">Select **Create**.</span></span>

<span data-ttu-id="f4b5c-148">Azure maakt het profiel en het eindpunt.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-148">Azure creates the profile and endpoint.</span></span> <span data-ttu-id="f4b5c-149">Het nieuwe eindpunt wordt weergegeven in de lijst **Eindpunten** op dezelfde pagina, wanneer het de status **Actief** heeft.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-149">The new endpoint appears in the **Endpoints** list on the same page, and when it's provisioned the status is **Running**.</span></span>

![Nieuw eindpunt in lijst](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-the-cdn-endpoint"></a><span data-ttu-id="f4b5c-151">Het CDN-eindpunt testen</span><span class="sxs-lookup"><span data-stu-id="f4b5c-151">Test the CDN endpoint</span></span>

<span data-ttu-id="f4b5c-152">Als u de prijscategorie Verizon hebt geselecteerd, duurt het doorgaans ongeveer 90 minuten voor het eindpunt is ingericht.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="f4b5c-153">In Akamai duurt het inrichten enkele minuten</span><span class="sxs-lookup"><span data-stu-id="f4b5c-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="f4b5c-154">De voorbeeld-app heeft een `index.html`-bestand en de mappen *css*, *img* en *js* met andere statische assets.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-154">The sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="f4b5c-155">De inhoudspaden voor al deze bestanden zijn op het CDN-eindpunt hetzelfde.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-155">The content paths for all of these files are the same at the CDN endpoint.</span></span> <span data-ttu-id="f4b5c-156">De volgende URL's bieden bijvoorbeeld toegang tot het bestand *bootstrap.css* in de map *css*:</span><span class="sxs-lookup"><span data-stu-id="f4b5c-156">For example, both of the following URLs access the *bootstrap.css* file in the *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="f4b5c-157">Navigeer in een browser naar de volgende URL:</span><span class="sxs-lookup"><span data-stu-id="f4b5c-157">Navigate a browser to the following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![Startpagina van voorbeeldapp waarvoor de gegevens vanuit CDN worden geleverd](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="f4b5c-159">U ziet dat dezelfde pagina die u eerder in een Azure-web-app hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-159">You see the same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="f4b5c-160">Azure CDN is opgehaald van de oorsprong web-app activa en is behoeve van het CDN-eindpunt</span><span class="sxs-lookup"><span data-stu-id="f4b5c-160">Azure CDN has retrieved the origin web app's assets and is serving them from the CDN endpoint</span></span>

<span data-ttu-id="f4b5c-161">Vernieuw de pagina om ervoor te zorgen dat deze pagina is opgeslagen in de cache in het CDN.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-161">To ensure that this page is cached in the CDN, refresh the page.</span></span> <span data-ttu-id="f4b5c-162">Er zijn soms twee aanvragen van hetzelfde asset vereist voordat het CDN de gevraagde inhoud in de cache opslaat.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-162">Two requests for the same asset are sometimes required for the CDN to cache the requested content.</span></span>

<span data-ttu-id="f4b5c-163">Zie voor meer informatie over het maken van Azure CDN-profielen en -eindpunten [Aan de slag met Azure CDN](../cdn/cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="f4b5c-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-the-cdn"></a><span data-ttu-id="f4b5c-164">Het CDN leegmaken</span><span class="sxs-lookup"><span data-stu-id="f4b5c-164">Purge the CDN</span></span>

<span data-ttu-id="f4b5c-165">Het CDN vernieuwt periodiek de behorende resources uit de oorspronkelijke web-app op basis van de configuratie van de time-to-live (TTL).</span><span class="sxs-lookup"><span data-stu-id="f4b5c-165">The CDN periodically refreshes its resources from the origin web app based on the time-to-live (TTL) configuration.</span></span> <span data-ttu-id="f4b5c-166">De standaard TTL-waarde is zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-166">The default TTL is seven days.</span></span>

<span data-ttu-id="f4b5c-167">Soms moet u wellicht het CDN vernieuwen voordat de TTL is verlopen. Bijvoorbeeld wanneer u bijgewerkte inhoud in de web-app implementeert.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-167">At times you might need to refresh the CDN before the TTL expiration -- for example, when you deploy updated content to the web app.</span></span> <span data-ttu-id="f4b5c-168">U kunt de resources in het CDN handmatig opschonen om te vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-168">To trigger a refresh, you can manually purge the CDN resources.</span></span> 

<span data-ttu-id="f4b5c-169">In dit gedeelte van de zelfstudie implementeert u een wijziging in de web-app en schoont u het CDN op zodat de bijbehorende cache wordt vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-169">In this section of the tutorial, you deploy a change to the web app and purge the CDN to trigger the CDN to refresh its cache.</span></span>

### <a name="deploy-a-change-to-the-web-app"></a><span data-ttu-id="f4b5c-170">Een wijziging implementeren in de web-app</span><span class="sxs-lookup"><span data-stu-id="f4b5c-170">Deploy a change to the web app</span></span>

<span data-ttu-id="f4b5c-171">Open het bestand `index.html` en voeg toe '- V2' toe aan de kop H1, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f4b5c-171">Open the `index.html` file and add "- V2" to the H1 heading, as shown in the following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="f4b5c-172">Voer uw wijziging door en implementeer deze naar de web-app.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-172">Commit your change and deploy it to the web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="f4b5c-173">Als de implementatie is voltooid, ziet u de wijziging als u naar de URL vn de web-app bladert.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-173">Once deployment has completed, browse to the web app URL and you see the change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

![V2 in de titel van de web-app](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="f4b5c-175">Als u naar de CDN-eindpunt-URL van de startpagina bladert, wordt de wijziging niet weergegeven omdat de in de cache opgeslagen versie in het CDN nog niet is verlopen.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-175">Browse to the CDN endpoint URL for the home page and you don't see the change because the cached version in the CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![Geen V2 in de titel van het CDN](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-the-cdn-in-the-portal"></a><span data-ttu-id="f4b5c-177">Het CDN leegmaken in de portal</span><span class="sxs-lookup"><span data-stu-id="f4b5c-177">Purge the CDN in the portal</span></span>

<span data-ttu-id="f4b5c-178">Schoon het CDN op zodat het de in de cache opgeslagen versie vernieuwt.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-178">To trigger the CDN to update its cached version, purge the CDN.</span></span>

<span data-ttu-id="f4b5c-179">Selecteer in de linkernavigatie in de portal de optie **Resourcegroepen** en selecteer vervolgens de resourcegroep die u hebt gemaakt voor uw web-app (myResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="f4b5c-179">In the portal left navigation, select **Resource groups**, and then select the resource group that you created for your web app (myResourceGroup).</span></span>

![Resourcegroep selecteren](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="f4b5c-181">Selecteer uw CDN-eindpunt in de lijst met resources.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-181">In the list of resources, select your CDN endpoint.</span></span>

![Eindpunt selecteren](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="f4b5c-183">Klik boven aan de pagina **Eindpunt** op **Leegmaken**.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-183">At the top of the **Endpoint** page, click **Purge**.</span></span>

![Leegmaken selecteren](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="f4b5c-185">Typ u de inhoudspaden die u wilt leegmaken.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-185">Enter the content paths you wish to purge.</span></span> <span data-ttu-id="f4b5c-186">Als u een afzonderlijk bestand wilt verwijderen, geeft u het volledige bestandspad door. Als u een map wilt leegmaken en vernieuwen, geeft u een padsegment door.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-186">You can pass a complete file path to purge an individual file, or a path segment to purge and refresh all content in a folder.</span></span> <span data-ttu-id="f4b5c-187">Zorg ervoor dat `index.html` een van de paden is, gezien u deze hebt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-187">Since you changed `index.html`, make sure that is one of the paths.</span></span>

<span data-ttu-id="f4b5c-188">Klik onder aan de pagina op **Leegmaken**.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-188">At the bottom of the page, select **Purge**.</span></span>

![Pagina leegmaken](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-the-cdn-is-updated"></a><span data-ttu-id="f4b5c-190">Controleren of het CDN is bijgewerkt</span><span class="sxs-lookup"><span data-stu-id="f4b5c-190">Verify that the CDN is updated</span></span>

<span data-ttu-id="f4b5c-191">Wacht totdat de aanvraag voor het leegmaken is verwerkt. Dit duurt doorgaans enkele minuten.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-191">Wait until the purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="f4b5c-192">Selecteer het belpictogram boven aan de pagina om de huidige status te bekijken.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-192">To see the current status, select the bell icon at the top of the page.</span></span> 

![Melding voor leegmaken](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="f4b5c-194">Blader naar de URL van het CDN-eindpunt voor `index.html`. U ziet nu de V2 die u hebt toegevoegd aan de titel op de startpagina.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-194">Browse to the CDN endpoint URL for `index.html`, and now you see the V2 that you added to the title on the home page.</span></span> <span data-ttu-id="f4b5c-195">U ziet dat de CDN-cache is vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-195">This shows that the CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![V2 in de titel van het CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="f4b5c-197">Zie voor meer informatie [Een Azure CDN-eindpunt leegmaken](../cdn/cdn-purge-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="f4b5c-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-to-version-content"></a><span data-ttu-id="f4b5c-198">Queryreeksen gebruiken om inhoud een versie te geven</span><span class="sxs-lookup"><span data-stu-id="f4b5c-198">Use query strings to version content</span></span>

<span data-ttu-id="f4b5c-199">Het Azure CDN biedt de volgende opties voor cachegedrag:</span><span class="sxs-lookup"><span data-stu-id="f4b5c-199">The Azure CDN offers the following caching behavior options:</span></span>

* <span data-ttu-id="f4b5c-200">Queryreeksen negeren</span><span class="sxs-lookup"><span data-stu-id="f4b5c-200">Ignore query strings</span></span>
* <span data-ttu-id="f4b5c-201">Queryreeksen in de cache opslaan overslaan</span><span class="sxs-lookup"><span data-stu-id="f4b5c-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="f4b5c-202">Elke unieke URL in de cache opslaan</span><span class="sxs-lookup"><span data-stu-id="f4b5c-202">Cache every unique URL</span></span> 

<span data-ttu-id="f4b5c-203">De eerste hiervan is de standaard, wat betekent dat er slechts één versie van een asset ongeacht de queryreeks in de URL-cache.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-203">The first of these is the default, which means there is only one cached version of an asset regardless of the query string in the URL.</span></span> 

<span data-ttu-id="f4b5c-204">In dit gedeelte van de zelfstudie wijzigt u het cachegedrag zodat elke unieke URL in de cache wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-204">In this section of the tutorial, you change the caching behavior to cache every unique URL.</span></span>

### <a name="change-the-cache-behavior"></a><span data-ttu-id="f4b5c-205">Het gedrag van de cache wijzigen</span><span class="sxs-lookup"><span data-stu-id="f4b5c-205">Change the cache behavior</span></span>

<span data-ttu-id="f4b5c-206">Selecteer in de Azure Portal op de pagina **CDN-eindpunt** de optie **Cache**.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-206">In the Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="f4b5c-207">Selecteer **Elke unieke URL in de cache opslaan** in de vervolgkeuzelijst **Cachegedrag van queryreeks**.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-207">Select **Cache every unique URL** from the **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="f4b5c-208">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-208">Select **Save**.</span></span>

![Selecteer cachegedrag van queryreeks](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="f4b5c-210">Controleren of de unieke URL's afzonderlijk in de cache worden opgeslagen</span><span class="sxs-lookup"><span data-stu-id="f4b5c-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="f4b5c-211">Navigeer in een browser naar de startpagina op het CDN-eindpunt, maar de volgende queryreeks toe:</span><span class="sxs-lookup"><span data-stu-id="f4b5c-211">In a browser, navigate to the home page at the CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="f4b5c-212">Het CDN retourneert de huidige inhoud van de web-app, met 'V2' in de kop.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-212">The CDN returns the current web app content, which includes "V2" in the heading.</span></span> 

<span data-ttu-id="f4b5c-213">Vernieuw de pagina om ervoor te zorgen dat deze pagina is opgeslagen in de cache in het CDN.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-213">To ensure that this page is cached in the CDN, refresh the page.</span></span> 

<span data-ttu-id="f4b5c-214">Open `index.html`, wijzig 'V2' in 'V3' en implementeer de wijziging.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-214">Open `index.html` and change "V2" to "V3", and deploy the change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="f4b5c-215">Ga in een browser naar de URL van het CDN-eindpunt met een nieuwe querytekenreeks zoals `q=2`.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-215">In a browser, go to the CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="f4b5c-216">Het CDN haalt het huidige `index.html`-bestand op en 'V3' wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-216">The CDN gets the current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="f4b5c-217">Als u echter naar het CDN-eindpunt navigeert met de querytekenreeks `q=1`, ziet u 'V2'.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-217">But if you navigate to the CDN endpoint with the `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![V3 in de titel in het CDN, queryreeks 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![V2 in de titel in het CDN, queryreeks 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="f4b5c-220">Deze uitvoer toont elke queryreeks anders wordt behandeld:</span><span class="sxs-lookup"><span data-stu-id="f4b5c-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="f4b5c-221">q = 1 werd gebruikt voorafgaand aan, zodat inhoud in cache (V2) worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="f4b5c-222">q = 2 is er nieuw is, zodat de meest recente inhoud voor web-app zijn opgehaald en (V3) geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-222">q=2 is new, so the latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="f4b5c-223">Zie [Cachegedrag in Azure CDN bepalen met queryreeksen](../cdn/cdn-query-string.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-to-a-cdn-endpoint"></a><span data-ttu-id="f4b5c-224">Een aangepast domein aan een CDN-eindpunt toewijzen</span><span class="sxs-lookup"><span data-stu-id="f4b5c-224">Map a custom domain to a CDN endpoint</span></span>

<span data-ttu-id="f4b5c-225">U wijst uw aangepaste domein toe aan uw CDN-eindpunt door een CNAME-record te maken.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-225">You'll map your custom domain to your CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="f4b5c-226">Een CNAME-record is een DNS-functie die een brondomein toewijst aan een doeldomein.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-226">A CNAME record is a DNS feature that maps a source domain to a destination domain.</span></span> <span data-ttu-id="f4b5c-227">U kunt bijvoorbeeld `cdn.contoso.com` of `static.contoso.com` toewijzen aan `contoso.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` to `contoso.azureedge.net`.</span></span>

<span data-ttu-id="f4b5c-228">Als u geen aangepaste domeinnaam hebt, overweeg dan de [Zelfstudie over App Service-domeinen](custom-dns-web-site-buydomains-web-app.md) te volgen om een domein aan te schaffen met de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-228">If you don't have a custom domain, consider following the [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) to purchase a domain using the Azure portal.</span></span> 

### <a name="find-the-hostname-to-use-with-the-cname"></a><span data-ttu-id="f4b5c-229">De hostnaam voor gebruik met de CNAME vinden</span><span class="sxs-lookup"><span data-stu-id="f4b5c-229">Find the hostname to use with the CNAME</span></span>

<span data-ttu-id="f4b5c-230">Zorg er in de Azure Portal op de pagina **Eindpunt** voor dat **Overzicht** is geselecteerd in de navigatiebalk aan de linkerkant en selecteer vervolgens de knop **+ Aangepast domein** boven aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-230">In the Azure portal **Endpoint** page, make sure **Overview** is selected in the left navigation, and then select the **+ Custom Domain** button at the top of the page.</span></span>

![Aangepast domein toevoegen selecteren](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="f4b5c-232">Op de pagina **Een aangepast domein toevoegen** ziet u de naam van de eindpunthost die u kunt gebruiken om een CNAME-record te maken.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-232">In the **Add a custom domain** page, you see the endpoint host name to use in creating a CNAME record.</span></span> <span data-ttu-id="f4b5c-233">De hostnaam is afgeleid van de URL van uw CDN-eindpunt: **&lt;EndpointName>. azureedge.net**.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-233">The host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![Een domeinpagina toevoegen](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-the-cname-with-your-domain-registrar"></a><span data-ttu-id="f4b5c-235">De CNAME configureren met uw domeinregistrar</span><span class="sxs-lookup"><span data-stu-id="f4b5c-235">Configure the CNAME with your domain registrar</span></span>

<span data-ttu-id="f4b5c-236">Navigeer naar de website van uw domeinregistrar en ga naar het gedeelte voor het maken van DNS-records.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-236">Navigate to your domain registrar's web site, and locate the section for creating DNS records.</span></span> <span data-ttu-id="f4b5c-237">U vindt dit in een gedeelte zoals **Domeinnaam**, **DNS** of **Serverbeheernaam**.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="f4b5c-238">Zoek het gedeelte voor het beheren van CNAME's.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-238">Find the section for managing CNAMEs.</span></span> <span data-ttu-id="f4b5c-239">Mogelijk moet u naar een pagina met geavanceerde instellingen gaan en de woorden CNAME, Alias of Subdomeinen zoeken.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-239">You may have to go to an advanced settings page and look for the words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="f4b5c-240">Een CNAME-record maken die uw gekozen subdomein toegewezen (bijvoorbeeld **statische** of **cdn**) naar de **eindpunt hostnaam** eerder in de portal weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) to the **Endpoint host name** shown earlier in the portal.</span></span> 

### <a name="enter-the-custom-domain-in-azure"></a><span data-ttu-id="f4b5c-241">Voer het aangepast domein in Azure in</span><span class="sxs-lookup"><span data-stu-id="f4b5c-241">Enter the custom domain in Azure</span></span>

<span data-ttu-id="f4b5c-242">Ga terug naar de pagina **Een aangepast domein toevoegen** en voer in het dialoogvenster uw aangepaste domein in, inclusief het subdomein.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-242">Return to the **Add a custom domain** page, and enter your custom domain, including the subdomain, in the dialog box.</span></span> <span data-ttu-id="f4b5c-243">Geef bijvoorbeeld `cdn.contoso.com` op.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="f4b5c-244">Azure controleert of de CNAME-record voor de domeinnaam die u hebt ingevoerd bestaat.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-244">Azure verifies that the CNAME record exists for the domain name you have entered.</span></span> <span data-ttu-id="f4b5c-245">Als de CNAME juist is, wordt uw aangepaste domein gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-245">If the CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="f4b5c-246">Het even kan duren voordat de CNAME-record is doorgeven aan de naamservers op het internet.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-246">It can take time for the CNAME record to propagate to name servers on the Internet.</span></span> <span data-ttu-id="f4b5c-247">Als uw domein is niet onmiddellijk gevalideerd, wacht een paar minuten en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-the-custom-domain"></a><span data-ttu-id="f4b5c-248">Het aangepaste domein testen</span><span class="sxs-lookup"><span data-stu-id="f4b5c-248">Test the custom domain</span></span>

<span data-ttu-id="f4b5c-249">Ga in een browser naar het bestand `index.html` op uw aangepaste domein (bijvoorbeeld `cdn.contoso.com/index.html`) om te controleren of het resultaat hetzelfde is als wanneer u rechtstreeks naar `<endpointname>azureedge.net/index.html` gaat.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-249">In a browser, navigate to the `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) to verify that the result is the same as when you go directly to `<endpointname>azureedge.net/index.html`.</span></span>

![Startpagina van voorbeeldapp met URL van aangepast domein](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="f4b5c-251">Zie voor meer informatie [Azure CDN-inhoud toewijzen aan een aangepast domein](../cdn/cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="f4b5c-251">For more information, see [Map Azure CDN content to a custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="f4b5c-252">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f4b5c-252">Next steps</span></span>

<span data-ttu-id="f4b5c-253">Wat u hebt geleerd:</span><span class="sxs-lookup"><span data-stu-id="f4b5c-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f4b5c-254">Een CDN-eindpunt maken.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="f4b5c-255">Assets in cache vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="f4b5c-256">Queryreeksen gebruiken voor het beheren van versies in cache.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-256">Use query strings to control cached versions.</span></span>
> * <span data-ttu-id="f4b5c-257">Een aangepast domein gebruiken voor het CDN-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="f4b5c-257">Use a custom domain for the CDN endpoint.</span></span>

<span data-ttu-id="f4b5c-258">Meer informatie over het optimaliseren van CDN in de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="f4b5c-258">Learn how to optimize CDN performance in the following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f4b5c-259">De prestaties verbeteren door bestanden in Azure CDN te comprimeren</span><span class="sxs-lookup"><span data-stu-id="f4b5c-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="f4b5c-260">Vooraf assets op een Azure CDN-eindpunt laden</span><span class="sxs-lookup"><span data-stu-id="f4b5c-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
