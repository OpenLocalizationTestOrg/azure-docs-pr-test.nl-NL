---
title: een actieve DNS-server aaaMigrate naam tooAzure App Service | Microsoft Docs
description: Meer informatie over hoe een aangepaste DNS-domeinnaam al tooa toegewezen is toomigrate live site tooAzure App Service zonder uitvaltijd.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a><span data-ttu-id="00b8a-103">Migreren van een actieve DNS-naam tooAzure App Service</span><span class="sxs-lookup"><span data-stu-id="00b8a-103">Migrate an active DNS name tooAzure App Service</span></span>

<span data-ttu-id="00b8a-104">Dit artikel laat zien hoe toomigrate een actieve DNS-server te naam[Azure App Service](../app-service/app-service-value-prop-what-is.md) zonder uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="00b8a-104">This article shows you how toomigrate an active DNS name too[Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="00b8a-105">Wanneer u een live site en de DNS-domein naam tooApp Service migreert, is al live verkeer voor de DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="00b8a-105">When you migrate a live site and its DNS domain name tooApp Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="00b8a-106">U kunt uitvaltijd in DNS-omzetting tijdens de migratie Hallo voorkomen door de optie preventief Hallo actieve DNS-naam tooyour App Service-app-binding.</span><span class="sxs-lookup"><span data-stu-id="00b8a-106">You can avoid downtime in DNS resolution during hello migration by binding hello active DNS name tooyour App Service app preemptively.</span></span>

<span data-ttu-id="00b8a-107">Als u niet over uitvaltijd in DNS-omzetting vastgesteld, Zie [toewijzen van een bestaande aangepaste DNS-naam tooAzure Web-Apps](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="00b8a-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00b8a-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="00b8a-108">Prerequisites</span></span>

<span data-ttu-id="00b8a-109">Deze instructies toocomplete:</span><span class="sxs-lookup"><span data-stu-id="00b8a-109">toocomplete this how-to:</span></span>

- <span data-ttu-id="00b8a-110">[Zorg ervoor dat uw app in App Service zich niet in de laag gratis](app-service-web-tutorial-custom-domain.md#checkpricing).</span><span class="sxs-lookup"><span data-stu-id="00b8a-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-hello-domain-name-preemptively"></a><span data-ttu-id="00b8a-111">Hallo-domeinnaam optie preventief binden</span><span class="sxs-lookup"><span data-stu-id="00b8a-111">Bind hello domain name preemptively</span></span>

<span data-ttu-id="00b8a-112">Wanneer u een aangepast domein optie preventief bindt, gedaan beide Hallo volgende voordat u wijzigingen aanbrengt in de DNS-records:</span><span class="sxs-lookup"><span data-stu-id="00b8a-112">When you bind a custom domain preemptively, you accomplish both of hello following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="00b8a-113">Domein verifiëren</span><span class="sxs-lookup"><span data-stu-id="00b8a-113">Verify domain ownership</span></span>
- <span data-ttu-id="00b8a-114">Hallo-domeinnaam voor uw app inschakelen</span><span class="sxs-lookup"><span data-stu-id="00b8a-114">Enable hello domain name for your app</span></span>

<span data-ttu-id="00b8a-115">Wanneer u ten slotte uw aangepaste DNS-naam van de oude site toohello App Service-app van Hallo migreert, zal er geen uitvaltijd in DNS-omzetting.</span><span class="sxs-lookup"><span data-stu-id="00b8a-115">When you finally migrate your custom DNS name from hello old site toohello App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="00b8a-116">Domein verificatie-record maken</span><span class="sxs-lookup"><span data-stu-id="00b8a-116">Create domain verification record</span></span>

<span data-ttu-id="00b8a-117">tooverify domein eigendom, Add een TXT-record.</span><span class="sxs-lookup"><span data-stu-id="00b8a-117">tooverify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="00b8a-118">Hallo TXT-record wordt toegewezen uit _awverify.&lt; subdomein >_ too_&lt;appname >. azurewebsites.net_.</span><span class="sxs-lookup"><span data-stu-id="00b8a-118">hello TXT record maps from _awverify.&lt;subdomain>_ too_&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="00b8a-119">Hallo TXT-record u moet, is afhankelijk van Hallo gewenste toomigrate van DNS-record.</span><span class="sxs-lookup"><span data-stu-id="00b8a-119">hello TXT record you need depends on hello DNS record you want toomigrate.</span></span> <span data-ttu-id="00b8a-120">Zie voor voorbeelden Hallo tabel (`@` doorgaans vertegenwoordigt hoofddomein Hallo):</span><span class="sxs-lookup"><span data-stu-id="00b8a-120">For examples, see hello following table (`@` typically represents hello root domain):</span></span>  

| <span data-ttu-id="00b8a-121">Voorbeeld van DNS-record</span><span class="sxs-lookup"><span data-stu-id="00b8a-121">DNS record example</span></span> | <span data-ttu-id="00b8a-122">TXT-Host</span><span class="sxs-lookup"><span data-stu-id="00b8a-122">TXT Host</span></span> | <span data-ttu-id="00b8a-123">TXT-waarde</span><span class="sxs-lookup"><span data-stu-id="00b8a-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="00b8a-124">@ (root)</span><span class="sxs-lookup"><span data-stu-id="00b8a-124">@ (root)</span></span> | <span data-ttu-id="00b8a-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="00b8a-125">_awverify_</span></span> | <span data-ttu-id="00b8a-126">_&lt;AppName >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="00b8a-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="00b8a-127">www (sub)</span><span class="sxs-lookup"><span data-stu-id="00b8a-127">www (sub)</span></span> | <span data-ttu-id="00b8a-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="00b8a-128">_awverify.www_</span></span> | <span data-ttu-id="00b8a-129">_&lt;AppName >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="00b8a-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="00b8a-130">\*(jokertekens)</span><span class="sxs-lookup"><span data-stu-id="00b8a-130">\* (wildcard)</span></span> | <span data-ttu-id="00b8a-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="00b8a-131">_awverify.\*_</span></span> | <span data-ttu-id="00b8a-132">_&lt;AppName >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="00b8a-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="00b8a-133">Houd er rekening mee Hallo recordtype Hallo DNS-naam die u wilt dat toomigrate in uw pagina DNS-records.</span><span class="sxs-lookup"><span data-stu-id="00b8a-133">In your DNS records page, note hello record type of hello DNS name you want toomigrate.</span></span> <span data-ttu-id="00b8a-134">App Service biedt ondersteuning voor toewijzingen van CNAME- en A-records.</span><span class="sxs-lookup"><span data-stu-id="00b8a-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-hello-domain-for-your-app"></a><span data-ttu-id="00b8a-135">Hallo-domein voor uw app inschakelen</span><span class="sxs-lookup"><span data-stu-id="00b8a-135">Enable hello domain for your app</span></span>

<span data-ttu-id="00b8a-136">In Hallo [Azure-portal](https://portal.azure.com), linkernavigatiegedeelte van de pagina app Hallo Hallo in, selecteer **aangepaste domeinen**.</span><span class="sxs-lookup"><span data-stu-id="00b8a-136">In hello [Azure portal](https://portal.azure.com), in hello left navigation of hello app page, select **Custom domains**.</span></span> 

![Aangepast domein menu](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="00b8a-138">In Hallo **aangepaste domeinen** pagina, selecteer Hallo  **+**  pictogram volgende te**hostnaam toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="00b8a-138">In hello **Custom domains** page, select hello **+** icon next too**Add hostname**.</span></span>

![Hostnaam toevoegen](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="00b8a-140">Type Hallo volledig gekwalificeerde domeinnaam Hallo TXT-record, zoals wordt toegevoegd `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="00b8a-140">Type hello fully qualified domain name that you added hello TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="00b8a-141">Voor een jokertekendomein (zoals \*. contoso.com), kunt u een DNS-naam die overeenkomt met de Hallo jokertekendomein.</span><span class="sxs-lookup"><span data-stu-id="00b8a-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches hello wildcard domain.</span></span> 

<span data-ttu-id="00b8a-142">Selecteer **valideren**.</span><span class="sxs-lookup"><span data-stu-id="00b8a-142">Select **Validate**.</span></span>

<span data-ttu-id="00b8a-143">Hallo **hostnaam toevoegen** knop wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="00b8a-143">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="00b8a-144">Zorg ervoor dat **hostnaam recordtype** toohello DNS-recordtype gewenste toomigrate is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="00b8a-144">Make sure that **Hostname record type** is set toohello DNS record type you want toomigrate.</span></span>

<span data-ttu-id="00b8a-145">Selecteer **hostnaam toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="00b8a-145">Select **Add hostname**.</span></span>

![DNS-naam toohello app toevoegen](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="00b8a-147">Het kan even duren voor Hallo nieuwe hostnaam toobe weerspiegeld in Hallo-app **aangepaste domeinen** pagina.</span><span class="sxs-lookup"><span data-stu-id="00b8a-147">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="00b8a-148">Vernieuw Hallo browser tooupdate Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="00b8a-148">Try refreshing hello browser tooupdate hello data.</span></span>

![CNAME-record is toegevoegd](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="00b8a-150">Uw aangepaste DNS-naam is nu ingeschakeld in uw app in Azure.</span><span class="sxs-lookup"><span data-stu-id="00b8a-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-hello-active-dns-name"></a><span data-ttu-id="00b8a-151">Opnieuw toewijzen Hallo actieve DNS-naam</span><span class="sxs-lookup"><span data-stu-id="00b8a-151">Remap hello active DNS name</span></span>

<span data-ttu-id="00b8a-152">Hallo alleen ding links toodo is opnieuw toewijzen van uw actieve DNS-record toopoint tooApp Service.</span><span class="sxs-lookup"><span data-stu-id="00b8a-152">hello only thing left toodo is remapping your active DNS record toopoint tooApp Service.</span></span> <span data-ttu-id="00b8a-153">Rechts nu nog steeds verwijst tooyour oude site.</span><span class="sxs-lookup"><span data-stu-id="00b8a-153">Right now, it still points tooyour old site.</span></span>

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a><span data-ttu-id="00b8a-154">Kopiëren van de app Hallo IP-adres (alleen een record)</span><span class="sxs-lookup"><span data-stu-id="00b8a-154">Copy hello app's IP address (A record only)</span></span>

<span data-ttu-id="00b8a-155">Als u opnieuw van een CNAME-record toewijzen, moet u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="00b8a-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="00b8a-156">tooremap een A-record, moet u Hallo App Service-app van externe IP-adres, die wordt weergegeven in Hallo **aangepaste domeinen** pagina.</span><span class="sxs-lookup"><span data-stu-id="00b8a-156">tooremap an A record, you need hello App Service app's external IP address, which is shown in hello **Custom domains** page.</span></span>

<span data-ttu-id="00b8a-157">Sluit Hallo **hostnaam toevoegen** pagina door te selecteren **X** in de rechterbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="00b8a-157">Close hello **Add hostname** page by selecting **X** in hello upper-right corner.</span></span> 

<span data-ttu-id="00b8a-158">In Hallo **aangepaste domeinen** pagina, te kopiëren van de app Hallo IP-adres.</span><span class="sxs-lookup"><span data-stu-id="00b8a-158">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![Navigatie in de portal tooAzure app](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a><span data-ttu-id="00b8a-160">Hallo DNS-record bijwerken</span><span class="sxs-lookup"><span data-stu-id="00b8a-160">Update hello DNS record</span></span>

<span data-ttu-id="00b8a-161">Selecteer Hallo DNS-record tooremap terug in Hallo DNS-records pagina van de domeinprovider van uw.</span><span class="sxs-lookup"><span data-stu-id="00b8a-161">Back in hello DNS records page of your domain provider, select hello DNS record tooremap.</span></span>

<span data-ttu-id="00b8a-162">Voor Hallo `contoso.com` voorbeeld van domein hoofdmap, Hallo A of CNAME-record zoals Hallo voorbeelden in de volgende tabel Hallo opnieuw toewijzen:</span><span class="sxs-lookup"><span data-stu-id="00b8a-162">For hello `contoso.com` root domain example, remap hello A or CNAME record like hello examples in hello following table:</span></span> 

| <span data-ttu-id="00b8a-163">FQDN-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="00b8a-163">FQDN example</span></span> | <span data-ttu-id="00b8a-164">Recordtype</span><span class="sxs-lookup"><span data-stu-id="00b8a-164">Record type</span></span> | <span data-ttu-id="00b8a-165">Host</span><span class="sxs-lookup"><span data-stu-id="00b8a-165">Host</span></span> | <span data-ttu-id="00b8a-166">Waarde</span><span class="sxs-lookup"><span data-stu-id="00b8a-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="00b8a-167">Contoso.com (root)</span><span class="sxs-lookup"><span data-stu-id="00b8a-167">contoso.com (root)</span></span> | <span data-ttu-id="00b8a-168">A</span><span class="sxs-lookup"><span data-stu-id="00b8a-168">A</span></span> | `@` | <span data-ttu-id="00b8a-169">IP-adres uit [kopie Hallo app IP-adres](#info)</span><span class="sxs-lookup"><span data-stu-id="00b8a-169">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="00b8a-170">www.contoso.com (sub)</span><span class="sxs-lookup"><span data-stu-id="00b8a-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="00b8a-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="00b8a-171">CNAME</span></span> | `www` | <span data-ttu-id="00b8a-172">_&lt;AppName >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="00b8a-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="00b8a-173">\*. contoso.com (jokertekens)</span><span class="sxs-lookup"><span data-stu-id="00b8a-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="00b8a-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="00b8a-174">CNAME</span></span> | _\*_ | <span data-ttu-id="00b8a-175">_&lt;AppName >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="00b8a-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="00b8a-176">Uw instellingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="00b8a-176">Save your settings.</span></span>

<span data-ttu-id="00b8a-177">DNS-query's moeten beginnen met het oplossen van App Service-app tooyour onmiddellijk nadat de DNS-servers gebeurt.</span><span class="sxs-lookup"><span data-stu-id="00b8a-177">DNS queries should start resolving tooyour App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00b8a-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="00b8a-178">Next steps</span></span>

<span data-ttu-id="00b8a-179">Meer informatie over hoe toobind een aangepaste SSL-certificaat tooApp Service.</span><span class="sxs-lookup"><span data-stu-id="00b8a-179">Learn how toobind a custom SSL certificate tooApp Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="00b8a-180">Binden van een bestaande aangepaste SSL-certificaat tooAzure Web-Apps</span><span class="sxs-lookup"><span data-stu-id="00b8a-180">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
