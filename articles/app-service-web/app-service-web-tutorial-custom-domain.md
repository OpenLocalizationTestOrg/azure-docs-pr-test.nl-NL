---
title: een bestaande aangepaste DNS-server aaaMap naam tooAzure Web-Apps | Microsoft Docs
description: Meer informatie over hoe tooadd een bestaand domein voor aangepaste DNS-naam (vanity domein) tooa web-app, back-end voor mobiele app of API-app in Azure App Service.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a><span data-ttu-id="b71e9-103">Toewijzen van een bestaande aangepaste DNS-naam tooAzure Web-Apps</span><span class="sxs-lookup"><span data-stu-id="b71e9-103">Map an existing custom DNS name tooAzure Web Apps</span></span>

<span data-ttu-id="b71e9-104">[Azure Web Apps](app-service-web-overview.md) biedt een uiterst schaalbare webhostingservice met self-patchfunctie.</span><span class="sxs-lookup"><span data-stu-id="b71e9-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="b71e9-105">Deze zelfstudie leert u hoe toomap een bestaande aangepaste DNS-Server name tooAzure Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="b71e9-105">This tutorial shows you how toomap an existing custom DNS name tooAzure Web Apps.</span></span>

![Navigatie in de portal tooAzure app](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="b71e9-107">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="b71e9-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b71e9-108">Een subdomein toewijzen (bijvoorbeeld `www.contoso.com`) met behulp van een CNAME-record</span><span class="sxs-lookup"><span data-stu-id="b71e9-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="b71e9-109">Toewijzen van een hoofddomein (bijvoorbeeld `contoso.com`) met behulp van een A-record</span><span class="sxs-lookup"><span data-stu-id="b71e9-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="b71e9-110">Toewijzen van een jokertekendomein (bijvoorbeeld `*.contoso.com`) met behulp van een CNAME-record</span><span class="sxs-lookup"><span data-stu-id="b71e9-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="b71e9-111">Domein-toewijzing met scripts automatiseren</span><span class="sxs-lookup"><span data-stu-id="b71e9-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="b71e9-112">U kunt ofwel een **CNAME-record** of een **een record** toomap een aangepaste DNS-naam tooApp Service.</span><span class="sxs-lookup"><span data-stu-id="b71e9-112">You can use either a **CNAME record** or an **A record** toomap a custom DNS name tooApp Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="b71e9-113">Het is raadzaam dat u een CNAME voor alle aangepaste DNS-namen, behalve een hoofddomein (bijvoorbeeld `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="b71e9-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="b71e9-114">toomigrate een live site en de DNS-domein naam tooApp Service, Zie [migreren van een actieve DNS-naam tooAzure App Service](app-service-custom-domain-name-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="b71e9-114">toomigrate a live site and its DNS domain name tooApp Service, see [Migrate an active DNS name tooAzure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b71e9-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b71e9-115">Prerequisites</span></span>

<span data-ttu-id="b71e9-116">toocomplete in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="b71e9-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="b71e9-117">[Een App Service-app maken](/azure/app-service/), of gebruik een app die u hebt gemaakt voor een andere zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="b71e9-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="b71e9-118">Een domeinnaam kopen en controleer of dat u toegang toohello DNS-register hebt voor uw domeinprovider (zoals GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="b71e9-118">Purchase a domain name and make sure you have access toohello DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="b71e9-119">Bijvoorbeeld: tooadd DNS-vermeldingen voor `contoso.com` en `www.contoso.com`, moet u kunnen tooconfigure Hallo DNS-instellingen voor Hallo `contoso.com` hoofddomein.</span><span class="sxs-lookup"><span data-stu-id="b71e9-119">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must be able tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b71e9-120">Als u een bestaand domein, Geef een naam, kunt u geen [aanschaffen van een domein via Azure portal Hallo](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="b71e9-120">If you don't have an existing domain name, consider [purchasing a domain using hello Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-hello-app"></a><span data-ttu-id="b71e9-121">Hallo app voorbereiden</span><span class="sxs-lookup"><span data-stu-id="b71e9-121">Prepare hello app</span></span>

<span data-ttu-id="b71e9-122">een aangepaste DNS-naam tooa van web-app, web-app Hallo toomap [App Service-abonnement](https://azure.microsoft.com/pricing/details/app-service/) moet een betaald laag (**gedeelde**, **Basic**, **standaard**, of  **Premium**).</span><span class="sxs-lookup"><span data-stu-id="b71e9-122">toomap a custom DNS name tooa web app, hello web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="b71e9-123">In deze stap maakt ervoor u zorgen dat Hallo App Service-app in Hallo is prijscategorie ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b71e9-123">In this step, you make sure that hello App Service app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="b71e9-124">Meld u aan tooAzure</span><span class="sxs-lookup"><span data-stu-id="b71e9-124">Sign in tooAzure</span></span>

<span data-ttu-id="b71e9-125">Open Hallo [Azure-portal](https://portal.azure.com) en meld u aan met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="b71e9-125">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="b71e9-126">Navigeer in hello Azure-portal toohello app</span><span class="sxs-lookup"><span data-stu-id="b71e9-126">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="b71e9-127">Selecteer in het linkermenu Hallo **App Services**, en selecteer vervolgens de naam Hallo van Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="b71e9-127">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![Navigatie in de portal tooAzure app](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="b71e9-129">U ziet de pagina voor het beheren van App Service-app Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b71e9-129">You see hello management page of hello App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="b71e9-130">Hallo prijscategorie controleren</span><span class="sxs-lookup"><span data-stu-id="b71e9-130">Check hello pricing tier</span></span>

<span data-ttu-id="b71e9-131">Schuif in Hallo linkernavigatiebalk van de pagina app hello, toohello **instellingen** sectie en selecteer **opschalen (App Service-abonnement)**.</span><span class="sxs-lookup"><span data-stu-id="b71e9-131">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Omhoog schalen-menu](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="b71e9-133">de huidige tier Hallo-app wordt door een rand gemarkeerd.</span><span class="sxs-lookup"><span data-stu-id="b71e9-133">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="b71e9-134">Controleren of die Hallo-app niet Hallo toomake **vrije** laag.</span><span class="sxs-lookup"><span data-stu-id="b71e9-134">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="b71e9-135">Aangepaste DNS wordt niet ondersteund in Hallo **vrije** laag.</span><span class="sxs-lookup"><span data-stu-id="b71e9-135">Custom DNS is not supported in hello **Free** tier.</span></span> 

![Controleer de prijscategorie](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="b71e9-137">Hallo App Service-abonnement is niet als **vrije**, sluit Hallo **Kies uw prijscategorie** pagina en te overslaan[toewijzen van een CNAME-record](#cname).</span><span class="sxs-lookup"><span data-stu-id="b71e9-137">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="b71e9-138">Hallo opschalen met App Service-abonnement</span><span class="sxs-lookup"><span data-stu-id="b71e9-138">Scale up hello App Service plan</span></span>

<span data-ttu-id="b71e9-139">Selecteer een van de Hallo-free lagen (**gedeelde**, **Basic**, **standaard**, of **Premium**).</span><span class="sxs-lookup"><span data-stu-id="b71e9-139">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="b71e9-140">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="b71e9-140">Click **Select**.</span></span>

![Controleer de prijscategorie](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="b71e9-142">Wanneer u de volgende kennisgeving Hallo ziet, is Hallo schaalbewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b71e9-142">When you see hello following notification, hello scale operation is complete.</span></span>

![Schaal bewerking bevestigen](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="b71e9-144">Toewijzen van een CNAME-record</span><span class="sxs-lookup"><span data-stu-id="b71e9-144">Map a CNAME record</span></span>

<span data-ttu-id="b71e9-145">In de zelfstudie voorbeeld hello, u een CNAME-record voor Hallo toevoegen `www` subdomein (bijvoorbeeld `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="b71e9-145">In hello tutorial example, you add a CNAME record for hello `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="b71e9-146">Hallo CNAME-record maken</span><span class="sxs-lookup"><span data-stu-id="b71e9-146">Create hello CNAME record</span></span>

<span data-ttu-id="b71e9-147">Voeg een CNAME-record toomap een subdomein toohello app standaard hostnaam (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="b71e9-147">Add a CNAME record toomap a subdomain toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="b71e9-148">Voor Hallo `www.contoso.com` domein voorbeeld, Voeg een CNAME-record die Hallo-naam toegewezen `www` te`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="b71e9-148">For hello `www.contoso.com` domain example, add a CNAME record that maps hello name `www` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="b71e9-149">Nadat u Hallo CNAME toegevoegd, ziet de pagina Hallo DNS-records Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="b71e9-149">After you add hello CNAME, hello DNS records page looks like hello following example:</span></span>

![Navigatie in de portal tooAzure app](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a><span data-ttu-id="b71e9-151">Hallo CNAME-record toewijzen in Azure inschakelen</span><span class="sxs-lookup"><span data-stu-id="b71e9-151">Enable hello CNAME record mapping in Azure</span></span>

<span data-ttu-id="b71e9-152">Selecteer in de Hallo Hallo op de pagina app linkernavigatiebalk in hello Azure-portal, **aangepaste domeinen**.</span><span class="sxs-lookup"><span data-stu-id="b71e9-152">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Aangepast domein menu](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="b71e9-154">In Hallo **aangepaste domeinen** pagina van het Hallo-app toevoegen Hallo FQDN aangepaste DNS-naam (`www.contoso.com`) toohello lijst.</span><span class="sxs-lookup"><span data-stu-id="b71e9-154">In hello **Custom domains** page of hello app, add hello fully qualified custom DNS name (`www.contoso.com`) toohello list.</span></span>

<span data-ttu-id="b71e9-155">Selecteer Hallo  **+**  pictogram volgende te**hostnaam toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b71e9-155">Select hello **+** icon next too**Add hostname**.</span></span>

![Hostnaam toevoegen](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="b71e9-157">Type Hallo volledig gekwalificeerde domeinnaam dat u een CNAME-record, zoals toegevoegd `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="b71e9-157">Type hello fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="b71e9-158">Selecteer **valideren**.</span><span class="sxs-lookup"><span data-stu-id="b71e9-158">Select **Validate**.</span></span>

<span data-ttu-id="b71e9-159">Hallo **hostnaam toevoegen** knop wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="b71e9-159">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="b71e9-160">Zorg ervoor dat **hostnaam recordtype** te is ingesteld,**CNAME (www.example.com of elk subdomein)**.</span><span class="sxs-lookup"><span data-stu-id="b71e9-160">Make sure that **Hostname record type** is set too**CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="b71e9-161">Selecteer **hostnaam toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b71e9-161">Select **Add hostname**.</span></span>

![DNS-naam toohello app toevoegen](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="b71e9-163">Het kan even duren voor Hallo nieuwe hostnaam toobe weerspiegeld in Hallo-app **aangepaste domeinen** pagina.</span><span class="sxs-lookup"><span data-stu-id="b71e9-163">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="b71e9-164">Vernieuw Hallo browser tooupdate Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="b71e9-164">Try refreshing hello browser tooupdate hello data.</span></span>

![CNAME-record is toegevoegd](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="b71e9-166">Als u een stap gemist of hebt u een typefout gemaakt ergens eerder, ziet u een verificatiefout Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="b71e9-166">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![Fout bij verificatie](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="b71e9-168">Toewijzen van een A-record</span><span class="sxs-lookup"><span data-stu-id="b71e9-168">Map an A record</span></span>

<span data-ttu-id="b71e9-169">Hallo zelfstudie bijvoorbeeld u een A-record voor het hoofddomein Hallo toevoegen (bijvoorbeeld `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="b71e9-169">In hello tutorial example, you add an A record for hello root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a><span data-ttu-id="b71e9-170">Kopiëren van de app Hallo IP-adres</span><span class="sxs-lookup"><span data-stu-id="b71e9-170">Copy hello app's IP address</span></span>

<span data-ttu-id="b71e9-171">toomap een A-record, moet u het externe IP-adres Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="b71e9-171">toomap an A record, you need hello app's external IP address.</span></span> <span data-ttu-id="b71e9-172">U vindt dit IP-adres in van de app Hallo **aangepaste domeinen** pagina in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b71e9-172">You can find this IP address in hello app's **Custom domains** page in hello Azure portal.</span></span>

<span data-ttu-id="b71e9-173">Selecteer in de Hallo Hallo op de pagina app linkernavigatiebalk in hello Azure-portal, **aangepaste domeinen**.</span><span class="sxs-lookup"><span data-stu-id="b71e9-173">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Aangepast domein menu](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="b71e9-175">In Hallo **aangepaste domeinen** pagina, te kopiëren van de app Hallo IP-adres.</span><span class="sxs-lookup"><span data-stu-id="b71e9-175">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![Navigatie in de portal tooAzure app](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a><span data-ttu-id="b71e9-177">Hallo-A-record maken</span><span class="sxs-lookup"><span data-stu-id="b71e9-177">Create hello A record</span></span>

<span data-ttu-id="b71e9-178">toomap een A-record tooan-app Service-App vereist **twee** DNS-records:</span><span class="sxs-lookup"><span data-stu-id="b71e9-178">toomap an A record tooan app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="b71e9-179">Een **A** Noteer toomap toohello app IP-adres.</span><span class="sxs-lookup"><span data-stu-id="b71e9-179">An **A** record toomap toohello app's IP address.</span></span>
- <span data-ttu-id="b71e9-180">Een **TXT** toomap toohello app standaard hostnaam vastleggen `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="b71e9-180">A **TXT** record toomap toohello app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="b71e9-181">App Service gebruikt deze record alleen tijdens de configuratie, tooverify dat u Hallo aangepast domein bezit.</span><span class="sxs-lookup"><span data-stu-id="b71e9-181">App Service uses this record only at configuration time, tooverify that you own hello custom domain.</span></span> <span data-ttu-id="b71e9-182">Nadat u uw aangepaste domein is gevalideerd en geconfigureerd in App Service, kunt u deze TXT-record verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b71e9-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="b71e9-183">Voor Hallo `contoso.com` domein bijvoorbeeld Hallo A en TXT-records volgens de volgende tabel toohello maken (`@` doorgaans vertegenwoordigt hoofddomein Hallo).</span><span class="sxs-lookup"><span data-stu-id="b71e9-183">For hello `contoso.com` domain example, create hello A and TXT records according toohello following table (`@` typically represents hello root domain).</span></span> 

| <span data-ttu-id="b71e9-184">Recordtype</span><span class="sxs-lookup"><span data-stu-id="b71e9-184">Record type</span></span> | <span data-ttu-id="b71e9-185">Host</span><span class="sxs-lookup"><span data-stu-id="b71e9-185">Host</span></span> | <span data-ttu-id="b71e9-186">Waarde</span><span class="sxs-lookup"><span data-stu-id="b71e9-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="b71e9-187">A</span><span class="sxs-lookup"><span data-stu-id="b71e9-187">A</span></span> | `@` | <span data-ttu-id="b71e9-188">IP-adres uit [kopie Hallo app IP-adres](#info)</span><span class="sxs-lookup"><span data-stu-id="b71e9-188">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="b71e9-189">TXT</span><span class="sxs-lookup"><span data-stu-id="b71e9-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="b71e9-190">Wanneer Hallo records worden toegevoegd, ziet er Hallo pagina DNS-records Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="b71e9-190">When hello records are added, hello DNS records page looks like hello following example:</span></span>

![Pagina DNS-records](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a><span data-ttu-id="b71e9-192">Hallo de toewijzing van een record in Hallo app inschakelen</span><span class="sxs-lookup"><span data-stu-id="b71e9-192">Enable hello A record mapping in hello app</span></span>

<span data-ttu-id="b71e9-193">Terug in Hallo-app **aangepaste domeinen** pagina in hello Azure-portal, het toevoegen van Hallo FQDN aangepaste DNS-naam (bijvoorbeeld `contoso.com`) toohello lijst.</span><span class="sxs-lookup"><span data-stu-id="b71e9-193">Back in hello app's **Custom domains** page in hello Azure portal, add hello fully qualified custom DNS name (for example, `contoso.com`) toohello list.</span></span>

<span data-ttu-id="b71e9-194">Selecteer Hallo  **+**  pictogram volgende te**hostnaam toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b71e9-194">Select hello **+** icon next too**Add hostname**.</span></span>

![Hostnaam toevoegen](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="b71e9-196">Type Hallo volledig gekwalificeerde domeinnaam Hallo A-record voor, zoals wordt geconfigureerd `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="b71e9-196">Type hello fully qualified domain name that you configured hello A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="b71e9-197">Selecteer **valideren**.</span><span class="sxs-lookup"><span data-stu-id="b71e9-197">Select **Validate**.</span></span>

<span data-ttu-id="b71e9-198">Hallo **hostnaam toevoegen** knop wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="b71e9-198">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="b71e9-199">Zorg ervoor dat **hostnaam recordtype** te is ingesteld,**een record (example.com)**.</span><span class="sxs-lookup"><span data-stu-id="b71e9-199">Make sure that **Hostname record type** is set too**A record (example.com)**.</span></span>

<span data-ttu-id="b71e9-200">Selecteer **hostnaam toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b71e9-200">Select **Add hostname**.</span></span>

![DNS-naam toohello app toevoegen](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="b71e9-202">Het kan even duren voor Hallo nieuwe hostnaam toobe weerspiegeld in Hallo-app **aangepaste domeinen** pagina.</span><span class="sxs-lookup"><span data-stu-id="b71e9-202">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="b71e9-203">Vernieuw Hallo browser tooupdate Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="b71e9-203">Try refreshing hello browser tooupdate hello data.</span></span>

![Een record die is toegevoegd](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="b71e9-205">Als u een stap gemist of hebt u een typefout gemaakt ergens eerder, ziet u een verificatiefout Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="b71e9-205">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![Fout bij verificatie](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="b71e9-207">Een jokertekendomein toewijzen</span><span class="sxs-lookup"><span data-stu-id="b71e9-207">Map a wildcard domain</span></span>

<span data-ttu-id="b71e9-208">In de zelfstudie voorbeeld Hallo, wijst u een [jokertekens DNS-naam](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (bijvoorbeeld `*.contoso.com`) toohello App Service-app door een CNAME-record toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="b71e9-208">In hello tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) toohello App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="b71e9-209">Hallo CNAME-record maken</span><span class="sxs-lookup"><span data-stu-id="b71e9-209">Create hello CNAME record</span></span>

<span data-ttu-id="b71e9-210">Voeg een CNAME-record toomap een jokerteken naam toohello app standaard hostnaam (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="b71e9-210">Add a CNAME record toomap a wildcard name toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="b71e9-211">Voor Hallo `*.contoso.com` domein bijvoorbeeld Hallo CNAME-record wordt wijst de naam van de Hallo `*` te`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="b71e9-211">For hello `*.contoso.com` domain example, hello CNAME record will map hello name `*` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="b71e9-212">Wanneer Hallo CNAME wordt toegevoegd, ziet er Hallo pagina DNS-records Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="b71e9-212">When hello CNAME is added, hello DNS records page looks like hello following example:</span></span>

![Navigatie in de portal tooAzure app](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a><span data-ttu-id="b71e9-214">Hallo CNAME-record toewijzing in Hallo app inschakelen</span><span class="sxs-lookup"><span data-stu-id="b71e9-214">Enable hello CNAME record mapping in hello app</span></span>

<span data-ttu-id="b71e9-215">U kunt nu elk subdomein dat overeenkomt met de Hallo jokertekens naam toohello app toevoegen (bijvoorbeeld `sub1.contoso.com` en `sub2.contoso.com` overeen met `*.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="b71e9-215">You can now add any subdomain that matches hello wildcard name toohello app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="b71e9-216">Selecteer in de Hallo Hallo op de pagina app linkernavigatiebalk in hello Azure-portal, **aangepaste domeinen**.</span><span class="sxs-lookup"><span data-stu-id="b71e9-216">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Aangepast domein menu](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="b71e9-218">Selecteer Hallo  **+**  pictogram volgende te**hostnaam toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b71e9-218">Select hello **+** icon next too**Add hostname**.</span></span>

![Hostnaam toevoegen](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="b71e9-220">Typ een FQDN-naam die overeenkomt met de Hallo jokertekendomein (bijvoorbeeld `sub1.contoso.com`), en selecteer vervolgens **valideren**.</span><span class="sxs-lookup"><span data-stu-id="b71e9-220">Type a fully qualified domain name that matches hello wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="b71e9-221">Hallo **hostnaam toevoegen** knop wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="b71e9-221">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="b71e9-222">Zorg ervoor dat **hostnaam recordtype** te is ingesteld,**CNAME-record (www.example.com of elk subdomein)**.</span><span class="sxs-lookup"><span data-stu-id="b71e9-222">Make sure that **Hostname record type** is set too**CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="b71e9-223">Selecteer **hostnaam toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b71e9-223">Select **Add hostname**.</span></span>

![DNS-naam toohello app toevoegen](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="b71e9-225">Het kan even duren voor Hallo nieuwe hostnaam toobe weerspiegeld in Hallo-app **aangepaste domeinen** pagina.</span><span class="sxs-lookup"><span data-stu-id="b71e9-225">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="b71e9-226">Vernieuw Hallo browser tooupdate Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="b71e9-226">Try refreshing hello browser tooupdate hello data.</span></span>

<span data-ttu-id="b71e9-227">Selecteer Hallo  **+**  pictogram opnieuw tooadd een andere hostnaam die overeenkomt met de Hallo jokertekendomein.</span><span class="sxs-lookup"><span data-stu-id="b71e9-227">Select hello **+** icon again tooadd another hostname that matches hello wildcard domain.</span></span> <span data-ttu-id="b71e9-228">Bijvoorbeeld, Voeg `sub2.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="b71e9-228">For example, add `sub2.contoso.com`.</span></span>

![CNAME-record is toegevoegd](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="b71e9-230">In de browser testen</span><span class="sxs-lookup"><span data-stu-id="b71e9-230">Test in browser</span></span>

<span data-ttu-id="b71e9-231">Blader toohello DNS-namen die u eerder hebt geconfigureerd (bijvoorbeeld `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, en `sub2.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="b71e9-231">Browse toohello DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![Navigatie in de portal tooAzure app](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="b71e9-233">Automatiseren met behulp van scripts</span><span class="sxs-lookup"><span data-stu-id="b71e9-233">Automate with scripts</span></span>

<span data-ttu-id="b71e9-234">U kunt beheer van aangepaste domeinen met behulp van scripts, automatiseren met behulp van Hallo [Azure CLI](/cli/azure/install-azure-cli) of [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b71e9-234">You can automate management of custom domains with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="b71e9-235">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b71e9-235">Azure CLI</span></span> 

<span data-ttu-id="b71e9-236">Hallo volgende opdracht voegt een geconfigureerde aangepaste DNS-naam tooan App Service-app.</span><span class="sxs-lookup"><span data-stu-id="b71e9-236">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="b71e9-237">Zie voor meer informatie [toewijzen van een aangepast domein tooa web-app](scripts/app-service-cli-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="b71e9-237">For more information, see [Map a custom domain tooa web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="b71e9-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b71e9-238">Azure PowerShell</span></span> 

<span data-ttu-id="b71e9-239">Hallo volgende opdracht voegt een geconfigureerde aangepaste DNS-naam tooan App Service-app.</span><span class="sxs-lookup"><span data-stu-id="b71e9-239">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="b71e9-240">Zie voor meer informatie [toewijzen van een aangepast domein tooa web-app](scripts/app-service-powershell-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="b71e9-240">For more information, see [Assign a custom domain tooa web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b71e9-241">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b71e9-241">Next steps</span></span>

<span data-ttu-id="b71e9-242">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="b71e9-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b71e9-243">Een subdomein toewijzen met behulp van een CNAME-record</span><span class="sxs-lookup"><span data-stu-id="b71e9-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="b71e9-244">Een hoofddomein toewijzen met behulp van een A-record</span><span class="sxs-lookup"><span data-stu-id="b71e9-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="b71e9-245">Een jokertekendomein toewijzen met behulp van een CNAME-record</span><span class="sxs-lookup"><span data-stu-id="b71e9-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="b71e9-246">Domein-toewijzing met scripts automatiseren</span><span class="sxs-lookup"><span data-stu-id="b71e9-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="b71e9-247">De volgende zelfstudie toolearn toohello gaan hoe toobind een aangepaste SSL-certificaat tooa web-app.</span><span class="sxs-lookup"><span data-stu-id="b71e9-247">Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b71e9-248">Binden van een bestaande aangepaste SSL-certificaat tooAzure Web-Apps</span><span class="sxs-lookup"><span data-stu-id="b71e9-248">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
