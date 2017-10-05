---
title: Een bestaande aangepaste DNS-naam toegewezen aan Azure Web Apps | Microsoft Docs
description: Informatie over het toevoegen van een bestaande aangepaste DNS-domeinnaam (vanity domein) aan een web-app, back-end voor mobiele app of API-app in Azure App Service.
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
ms.openlocfilehash: 973cda462e8d258cc848e1036891c7f8af043102
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="map-an-existing-custom-dns-name-to-azure-web-apps"></a><span data-ttu-id="ea629-103">Een bestaande aangepaste DNS-naam toegewezen aan Azure-Web-Apps</span><span class="sxs-lookup"><span data-stu-id="ea629-103">Map an existing custom DNS name to Azure Web Apps</span></span>

<span data-ttu-id="ea629-104">[Azure Web Apps](app-service-web-overview.md) biedt een uiterst schaalbare webhostingservice met self-patchfunctie.</span><span class="sxs-lookup"><span data-stu-id="ea629-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="ea629-105">Deze zelfstudie laat zien hoe u een bestaande aangepaste DNS-naam toewijzen aan Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="ea629-105">This tutorial shows you how to map an existing custom DNS name to Azure Web Apps.</span></span>

![Navigatie naar Azure-app in de portal](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="ea629-107">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="ea629-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ea629-108">Een subdomein toewijzen (bijvoorbeeld `www.contoso.com`) met behulp van een CNAME-record</span><span class="sxs-lookup"><span data-stu-id="ea629-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="ea629-109">Toewijzen van een hoofddomein (bijvoorbeeld `contoso.com`) met behulp van een A-record</span><span class="sxs-lookup"><span data-stu-id="ea629-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="ea629-110">Toewijzen van een jokertekendomein (bijvoorbeeld `*.contoso.com`) met behulp van een CNAME-record</span><span class="sxs-lookup"><span data-stu-id="ea629-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="ea629-111">Domein-toewijzing met scripts automatiseren</span><span class="sxs-lookup"><span data-stu-id="ea629-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="ea629-112">U kunt ofwel een **CNAME-record** of een **een record** toewijzen van een aangepaste DNS-naam in App Service.</span><span class="sxs-lookup"><span data-stu-id="ea629-112">You can use either a **CNAME record** or an **A record** to map a custom DNS name to App Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="ea629-113">Het is raadzaam dat u een CNAME voor alle aangepaste DNS-namen, behalve een hoofddomein (bijvoorbeeld `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="ea629-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="ea629-114">Zie voor het migreren van een live site en de DNS-domeinnaam in App Service, [een actieve DNS-naam migreren naar Azure App Service](app-service-custom-domain-name-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="ea629-114">To migrate a live site and its DNS domain name to App Service, see [Migrate an active DNS name to Azure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea629-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ea629-115">Prerequisites</span></span>

<span data-ttu-id="ea629-116">Vereisten voor het voltooien van deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="ea629-116">To complete this tutorial:</span></span>

* <span data-ttu-id="ea629-117">[Een App Service-app maken](/azure/app-service/), of gebruik een app die u hebt gemaakt voor een andere zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="ea629-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="ea629-118">Een domeinnaam kopen en controleer of dat u toegang hebt tot het register DNS voor uw domeinprovider (zoals GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="ea629-118">Purchase a domain name and make sure you have access to the DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="ea629-119">Bijvoorbeeld, om toe te voegen DNS-vermeldingen voor `contoso.com` en `www.contoso.com`, moet u kunnen de DNS-instellingen configureren voor de `contoso.com` hoofddomein.</span><span class="sxs-lookup"><span data-stu-id="ea629-119">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must be able to configure the DNS settings for the `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ea629-120">Als u een bestaand domein, Geef een naam, kunt u geen [aanschaffen van een domein met de Azure portal](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="ea629-120">If you don't have an existing domain name, consider [purchasing a domain using the Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-the-app"></a><span data-ttu-id="ea629-121">De app voorbereiden</span><span class="sxs-lookup"><span data-stu-id="ea629-121">Prepare the app</span></span>

<span data-ttu-id="ea629-122">Een aangepaste DNS-naam toewijzen aan een web-app, de web-app van [App Service-abonnement](https://azure.microsoft.com/pricing/details/app-service/) moet een betaald laag (**gedeelde**, **Basic**, **standaard**, of  **Premium**).</span><span class="sxs-lookup"><span data-stu-id="ea629-122">To map a custom DNS name to a web app, the web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="ea629-123">In deze stap maakt ervoor u zorgen dat de App Service-app is in de ondersteunde prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="ea629-123">In this step, you make sure that the App Service app is in the supported pricing tier.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="ea629-124">Aanmelden bij Azure</span><span class="sxs-lookup"><span data-stu-id="ea629-124">Sign in to Azure</span></span>

<span data-ttu-id="ea629-125">Open de [Azure-portal](https://portal.azure.com) en meld u aan met uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="ea629-125">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-to-the-app-in-the-azure-portal"></a><span data-ttu-id="ea629-126">Navigeer naar de app in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="ea629-126">Navigate to the app in the Azure portal</span></span>

<span data-ttu-id="ea629-127">Selecteer in het menu links **App Services**, en selecteer vervolgens de naam van de app.</span><span class="sxs-lookup"><span data-stu-id="ea629-127">From the left menu, select **App Services**, and then select the name of the app.</span></span>

![Navigatie naar Azure-app in de portal](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="ea629-129">U ziet de beheerpagina van de App Service-app.</span><span class="sxs-lookup"><span data-stu-id="ea629-129">You see the management page of the App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-the-pricing-tier"></a><span data-ttu-id="ea629-130">Controleer de prijscategorie</span><span class="sxs-lookup"><span data-stu-id="ea629-130">Check the pricing tier</span></span>

<span data-ttu-id="ea629-131">Schuif in de navigatiebalk links van de app-pagina naar de **instellingen** sectie en selecteer **opschalen (App Service-abonnement)**.</span><span class="sxs-lookup"><span data-stu-id="ea629-131">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Omhoog schalen-menu](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="ea629-133">De huidige tier van de app wordt gemarkeerd door een rand.</span><span class="sxs-lookup"><span data-stu-id="ea629-133">The app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="ea629-134">Controleer of de app is niet in de **vrije** laag.</span><span class="sxs-lookup"><span data-stu-id="ea629-134">Check to make sure that the app is not in the **Free** tier.</span></span> <span data-ttu-id="ea629-135">Aangepaste DNS wordt niet ondersteund in de **vrije** laag.</span><span class="sxs-lookup"><span data-stu-id="ea629-135">Custom DNS is not supported in the **Free** tier.</span></span> 

![Controleer de prijscategorie](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="ea629-137">Als de App Service-abonnement niet **vrije**, sluit de **Kies uw prijscategorie** pagina en doorgaan met [toewijzen van een CNAME-record](#cname).</span><span class="sxs-lookup"><span data-stu-id="ea629-137">If the App Service plan is not **Free**, close the **Choose your pricing tier** page and skip to [Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-the-app-service-plan"></a><span data-ttu-id="ea629-138">De App Service-abonnement opschalen</span><span class="sxs-lookup"><span data-stu-id="ea629-138">Scale up the App Service plan</span></span>

<span data-ttu-id="ea629-139">Selecteer een van de lagen niet vrij (**gedeelde**, **Basic**, **standaard**, of **Premium**).</span><span class="sxs-lookup"><span data-stu-id="ea629-139">Select any of the non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="ea629-140">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="ea629-140">Click **Select**.</span></span>

![Controleer de prijscategorie](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="ea629-142">Wanneer u de volgende melding ziet, is de schaalbewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ea629-142">When you see the following notification, the scale operation is complete.</span></span>

![Schaal bewerking bevestigen](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="ea629-144">Toewijzen van een CNAME-record</span><span class="sxs-lookup"><span data-stu-id="ea629-144">Map a CNAME record</span></span>

<span data-ttu-id="ea629-145">In de zelfstudie voorbeeld voegt u toe een CNAME-record voor de `www` subdomein (bijvoorbeeld `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="ea629-145">In the tutorial example, you add a CNAME record for the `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-cname-record"></a><span data-ttu-id="ea629-146">De CNAME-record maken</span><span class="sxs-lookup"><span data-stu-id="ea629-146">Create the CNAME record</span></span>

<span data-ttu-id="ea629-147">Voeg een CNAME-record voor een subdomein toewijzen aan de app standaard hostnaam (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="ea629-147">Add a CNAME record to map a subdomain to the app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="ea629-148">Voor de `www.contoso.com` domein voorbeeld, Voeg een CNAME-record dat is toegewezen, de naam van de `www` naar `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="ea629-148">For the `www.contoso.com` domain example, add a CNAME record that maps the name `www` to `<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="ea629-149">Nadat u de CNAME toevoegt, wordt de pagina DNS-records lijkt op het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ea629-149">After you add the CNAME, the DNS records page looks like the following example:</span></span>

![Navigatie naar Azure-app in de portal](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-the-cname-record-mapping-in-azure"></a><span data-ttu-id="ea629-151">De toewijzing van de CNAME-record in Azure inschakelen</span><span class="sxs-lookup"><span data-stu-id="ea629-151">Enable the CNAME record mapping in Azure</span></span>

<span data-ttu-id="ea629-152">Selecteer in het linkernavigatievenster van de app-pagina in de Azure portal **aangepaste domeinen**.</span><span class="sxs-lookup"><span data-stu-id="ea629-152">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Aangepast domein menu](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="ea629-154">In de **aangepaste domeinen** pagina van de app toevoegen de volledig gekwalificeerde aangepaste DNS-naam (`www.contoso.com`) aan de lijst.</span><span class="sxs-lookup"><span data-stu-id="ea629-154">In the **Custom domains** page of the app, add the fully qualified custom DNS name (`www.contoso.com`) to the list.</span></span>

<span data-ttu-id="ea629-155">Selecteer de  **+**  pictogram naast **hostnaam toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ea629-155">Select the **+** icon next to **Add hostname**.</span></span>

![Hostnaam toevoegen](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="ea629-157">Typ de volledig gekwalificeerde domeinnaam dat u een CNAME-record, zoals toegevoegd `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="ea629-157">Type the fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="ea629-158">Selecteer **valideren**.</span><span class="sxs-lookup"><span data-stu-id="ea629-158">Select **Validate**.</span></span>

<span data-ttu-id="ea629-159">De **hostnaam toevoegen** knop wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="ea629-159">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="ea629-160">Zorg ervoor dat **hostnaam recordtype** is ingesteld op **CNAME (www.example.com of elk subdomein)**.</span><span class="sxs-lookup"><span data-stu-id="ea629-160">Make sure that **Hostname record type** is set to **CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="ea629-161">Selecteer **hostnaam toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ea629-161">Select **Add hostname**.</span></span>

![DNS-naam toevoegen aan de app.](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="ea629-163">Het kan even duren voor de nieuwe hostnaam worden weergegeven in de app **aangepaste domeinen** pagina.</span><span class="sxs-lookup"><span data-stu-id="ea629-163">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="ea629-164">Vernieuw de browser voor het bijwerken van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="ea629-164">Try refreshing the browser to update the data.</span></span>

![CNAME-record is toegevoegd](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="ea629-166">Als u een stap gemist of hebt u een typefout gemaakt ergens eerder, ziet u een fout bij verificatie van aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="ea629-166">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![Fout bij verificatie](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="ea629-168">Toewijzen van een A-record</span><span class="sxs-lookup"><span data-stu-id="ea629-168">Map an A record</span></span>

<span data-ttu-id="ea629-169">In de zelfstudie voorbeeld voegt u toe een A-record voor het hoofddomein (bijvoorbeeld `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="ea629-169">In the tutorial example, you add an A record for the root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-the-apps-ip-address"></a><span data-ttu-id="ea629-170">Kopiëren van de app IP-adres</span><span class="sxs-lookup"><span data-stu-id="ea629-170">Copy the app's IP address</span></span>

<span data-ttu-id="ea629-171">Als u wilt een A-record toewijzen, moet u het externe IP-adres van de app.</span><span class="sxs-lookup"><span data-stu-id="ea629-171">To map an A record, you need the app's external IP address.</span></span> <span data-ttu-id="ea629-172">U vindt dit IP-adres in van de app **aangepaste domeinen** pagina in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ea629-172">You can find this IP address in the app's **Custom domains** page in the Azure portal.</span></span>

<span data-ttu-id="ea629-173">Selecteer in het linkernavigatievenster van de app-pagina in de Azure portal **aangepaste domeinen**.</span><span class="sxs-lookup"><span data-stu-id="ea629-173">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Aangepast domein menu](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="ea629-175">In de **aangepaste domeinen** pagina, kopieert u de app IP-adres.</span><span class="sxs-lookup"><span data-stu-id="ea629-175">In the **Custom domains** page, copy the app's IP address.</span></span>

![Navigatie naar Azure-app in de portal](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-a-record"></a><span data-ttu-id="ea629-177">De A-record maken</span><span class="sxs-lookup"><span data-stu-id="ea629-177">Create the A record</span></span>

<span data-ttu-id="ea629-178">Als u wilt een A-record toewijzen aan een app, App-Service vereist **twee** DNS-records:</span><span class="sxs-lookup"><span data-stu-id="ea629-178">To map an A record to an app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="ea629-179">Een **A** record toewijzen aan IP-adres van de app.</span><span class="sxs-lookup"><span data-stu-id="ea629-179">An **A** record to map to the app's IP address.</span></span>
- <span data-ttu-id="ea629-180">Een **TXT** record toewijzen aan de app standaard hostnaam `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="ea629-180">A **TXT** record to map to the app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="ea629-181">App Service gebruikt deze record alleen tijdens de configuratie, om te controleren of de eigenaar van het aangepaste domein.</span><span class="sxs-lookup"><span data-stu-id="ea629-181">App Service uses this record only at configuration time, to verify that you own the custom domain.</span></span> <span data-ttu-id="ea629-182">Nadat u uw aangepaste domein is gevalideerd en geconfigureerd in App Service, kunt u deze TXT-record verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ea629-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="ea629-183">Voor de `contoso.com` domein bijvoorbeeld de A- en TXT-records overeenkomstig de volgende tabel maken (`@` vertegenwoordigt doorgaans het hoofddomein).</span><span class="sxs-lookup"><span data-stu-id="ea629-183">For the `contoso.com` domain example, create the A and TXT records according to the following table (`@` typically represents the root domain).</span></span> 

| <span data-ttu-id="ea629-184">Recordtype</span><span class="sxs-lookup"><span data-stu-id="ea629-184">Record type</span></span> | <span data-ttu-id="ea629-185">Host</span><span class="sxs-lookup"><span data-stu-id="ea629-185">Host</span></span> | <span data-ttu-id="ea629-186">Waarde</span><span class="sxs-lookup"><span data-stu-id="ea629-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="ea629-187">A</span><span class="sxs-lookup"><span data-stu-id="ea629-187">A</span></span> | `@` | <span data-ttu-id="ea629-188">IP-adres uit [kopiëren van de app IP-adres](#info)</span><span class="sxs-lookup"><span data-stu-id="ea629-188">IP address from [Copy the app's IP address](#info)</span></span> |
| <span data-ttu-id="ea629-189">TXT</span><span class="sxs-lookup"><span data-stu-id="ea629-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="ea629-190">Wanneer de records worden toegevoegd, wordt de pagina DNS-records lijkt op het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ea629-190">When the records are added, the DNS records page looks like the following example:</span></span>

![Pagina DNS-records](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-the-a-record-mapping-in-the-app"></a><span data-ttu-id="ea629-192">De toewijzing van een record in de app inschakelen</span><span class="sxs-lookup"><span data-stu-id="ea629-192">Enable the A record mapping in the app</span></span>

<span data-ttu-id="ea629-193">Terug in de app **aangepaste domeinen** pagina in de Azure portal, het toevoegen van de volledig gekwalificeerde aangepaste DNS-naam (bijvoorbeeld `contoso.com`) aan de lijst.</span><span class="sxs-lookup"><span data-stu-id="ea629-193">Back in the app's **Custom domains** page in the Azure portal, add the fully qualified custom DNS name (for example, `contoso.com`) to the list.</span></span>

<span data-ttu-id="ea629-194">Selecteer de  **+**  pictogram naast **hostnaam toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ea629-194">Select the **+** icon next to **Add hostname**.</span></span>

![Hostnaam toevoegen](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="ea629-196">Typ de volledig gekwalificeerde domeinnaam dat u de A-record, zoals geconfigureerd `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="ea629-196">Type the fully qualified domain name that you configured the A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="ea629-197">Selecteer **valideren**.</span><span class="sxs-lookup"><span data-stu-id="ea629-197">Select **Validate**.</span></span>

<span data-ttu-id="ea629-198">De **hostnaam toevoegen** knop wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="ea629-198">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="ea629-199">Zorg ervoor dat **hostnaam recordtype** is ingesteld op **een record (example.com)**.</span><span class="sxs-lookup"><span data-stu-id="ea629-199">Make sure that **Hostname record type** is set to **A record (example.com)**.</span></span>

<span data-ttu-id="ea629-200">Selecteer **hostnaam toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ea629-200">Select **Add hostname**.</span></span>

![DNS-naam toevoegen aan de app.](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="ea629-202">Het kan even duren voor de nieuwe hostnaam worden weergegeven in de app **aangepaste domeinen** pagina.</span><span class="sxs-lookup"><span data-stu-id="ea629-202">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="ea629-203">Vernieuw de browser voor het bijwerken van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="ea629-203">Try refreshing the browser to update the data.</span></span>

![Een record die is toegevoegd](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="ea629-205">Als u een stap gemist of hebt u een typefout gemaakt ergens eerder, ziet u een fout bij verificatie van aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="ea629-205">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![Fout bij verificatie](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="ea629-207">Een jokertekendomein toewijzen</span><span class="sxs-lookup"><span data-stu-id="ea629-207">Map a wildcard domain</span></span>

<span data-ttu-id="ea629-208">In de zelfstudie voorbeeld, wijst u een [jokertekens DNS-naam](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (bijvoorbeeld `*.contoso.com`) naar de App Service-app door een CNAME-record toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="ea629-208">In the tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) to the App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-cname-record"></a><span data-ttu-id="ea629-209">De CNAME-record maken</span><span class="sxs-lookup"><span data-stu-id="ea629-209">Create the CNAME record</span></span>

<span data-ttu-id="ea629-210">Voeg een CNAME-record de jokertekennaam van een om toe te wijzen hostnaam van de app-standaard (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="ea629-210">Add a CNAME record to map a wildcard name to the app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="ea629-211">Voor de `*.contoso.com` domein bijvoorbeeld de CNAME-record wordt de naam toewijzen `*` naar `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="ea629-211">For the `*.contoso.com` domain example, the CNAME record will map the name `*` to `<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="ea629-212">Wanneer de CNAME wordt toegevoegd, ziet de pagina DNS-records in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ea629-212">When the CNAME is added, the DNS records page looks like the following example:</span></span>

![Navigatie naar Azure-app in de portal](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-the-cname-record-mapping-in-the-app"></a><span data-ttu-id="ea629-214">De toewijzing van de CNAME-record in de app inschakelen</span><span class="sxs-lookup"><span data-stu-id="ea629-214">Enable the CNAME record mapping in the app</span></span>

<span data-ttu-id="ea629-215">U kunt nu elk subdomein dat overeenkomt met de jokertekennaam naar de app toevoegen (bijvoorbeeld `sub1.contoso.com` en `sub2.contoso.com` overeen met `*.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="ea629-215">You can now add any subdomain that matches the wildcard name to the app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="ea629-216">Selecteer in het linkernavigatievenster van de app-pagina in de Azure portal **aangepaste domeinen**.</span><span class="sxs-lookup"><span data-stu-id="ea629-216">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Aangepast domein menu](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="ea629-218">Selecteer de  **+**  pictogram naast **hostnaam toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ea629-218">Select the **+** icon next to **Add hostname**.</span></span>

![Hostnaam toevoegen](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="ea629-220">Typ een FQDN-naam die overeenkomt met het jokertekendomein (bijvoorbeeld `sub1.contoso.com`), en selecteer vervolgens **valideren**.</span><span class="sxs-lookup"><span data-stu-id="ea629-220">Type a fully qualified domain name that matches the wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="ea629-221">De **hostnaam toevoegen** knop wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="ea629-221">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="ea629-222">Zorg ervoor dat **hostnaam recordtype** is ingesteld op **CNAME-record (www.example.com of elk subdomein)**.</span><span class="sxs-lookup"><span data-stu-id="ea629-222">Make sure that **Hostname record type** is set to **CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="ea629-223">Selecteer **hostnaam toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ea629-223">Select **Add hostname**.</span></span>

![DNS-naam toevoegen aan de app.](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="ea629-225">Het kan even duren voor de nieuwe hostnaam worden weergegeven in de app **aangepaste domeinen** pagina.</span><span class="sxs-lookup"><span data-stu-id="ea629-225">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="ea629-226">Vernieuw de browser voor het bijwerken van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="ea629-226">Try refreshing the browser to update the data.</span></span>

<span data-ttu-id="ea629-227">Selecteer de  **+**  pictogram opnieuw naar een andere hostnaam die overeenkomt met het jokertekendomein toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ea629-227">Select the **+** icon again to add another hostname that matches the wildcard domain.</span></span> <span data-ttu-id="ea629-228">Bijvoorbeeld, Voeg `sub2.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="ea629-228">For example, add `sub2.contoso.com`.</span></span>

![CNAME-record is toegevoegd](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="ea629-230">In de browser testen</span><span class="sxs-lookup"><span data-stu-id="ea629-230">Test in browser</span></span>

<span data-ttu-id="ea629-231">Blader naar de DNS-namen die u eerder hebt geconfigureerd (bijvoorbeeld `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, en `sub2.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="ea629-231">Browse to the DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![Navigatie naar Azure-app in de portal](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="ea629-233">Automatiseren met behulp van scripts</span><span class="sxs-lookup"><span data-stu-id="ea629-233">Automate with scripts</span></span>

<span data-ttu-id="ea629-234">U kunt beheer van aangepaste domeinen met behulp van scripts, automatiseren met behulp van de [Azure CLI](/cli/azure/install-azure-cli) of [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ea629-234">You can automate management of custom domains with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="ea629-235">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ea629-235">Azure CLI</span></span> 

<span data-ttu-id="ea629-236">De volgende opdracht voegt een geconfigureerde aangepaste DNS-naam naar een App Service-app.</span><span class="sxs-lookup"><span data-stu-id="ea629-236">The following command adds a configured custom DNS name to an App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="ea629-237">Zie voor meer informatie [een aangepast domein toewijzen aan een web-app](scripts/app-service-cli-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="ea629-237">For more information, see [Map a custom domain to a web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="ea629-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea629-238">Azure PowerShell</span></span> 

<span data-ttu-id="ea629-239">De volgende opdracht voegt een geconfigureerde aangepaste DNS-naam naar een App Service-app.</span><span class="sxs-lookup"><span data-stu-id="ea629-239">The following command adds a configured custom DNS name to an App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="ea629-240">Zie voor meer informatie [een aangepast domein toewijzen aan een web-app](scripts/app-service-powershell-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="ea629-240">For more information, see [Assign a custom domain to a web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea629-241">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ea629-241">Next steps</span></span>

<span data-ttu-id="ea629-242">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="ea629-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ea629-243">Een subdomein toewijzen met behulp van een CNAME-record</span><span class="sxs-lookup"><span data-stu-id="ea629-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="ea629-244">Een hoofddomein toewijzen met behulp van een A-record</span><span class="sxs-lookup"><span data-stu-id="ea629-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="ea629-245">Een jokertekendomein toewijzen met behulp van een CNAME-record</span><span class="sxs-lookup"><span data-stu-id="ea629-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="ea629-246">Domein-toewijzing met scripts automatiseren</span><span class="sxs-lookup"><span data-stu-id="ea629-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="ea629-247">Ga naar de volgende zelfstudie voor meer informatie over hoe u een aangepaste SSL-certificaat binden aan een web-app.</span><span class="sxs-lookup"><span data-stu-id="ea629-247">Advance to the next tutorial to learn how to bind a custom SSL certificate to a web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ea629-248">Een bestaande aangepaste SSL-certificaat binden aan Azure-Web-Apps</span><span class="sxs-lookup"><span data-stu-id="ea629-248">Bind an existing custom SSL certificate to Azure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
