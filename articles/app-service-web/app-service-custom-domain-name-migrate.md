---
title: Een actieve DNS-naam migreren naar Azure App Service | Microsoft Docs
description: Informatie over het migreren van een aangepaste DNS-domeinnaam al aan een actieve site naar Azure App Service zonder uitvaltijd toegewezen is.
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
ms.openlocfilehash: 89308c1c684a639950467b72d26703cc07c50c14
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-an-active-dns-name-to-azure-app-service"></a><span data-ttu-id="23113-103">Een actieve DNS-naam migreren naar Azure App Service</span><span class="sxs-lookup"><span data-stu-id="23113-103">Migrate an active DNS name to Azure App Service</span></span>

<span data-ttu-id="23113-104">Dit artikel laat zien hoe u migreert van een actieve DNS-naam voor [Azure App Service](../app-service/app-service-value-prop-what-is.md) zonder uitvaltijd.</span><span class="sxs-lookup"><span data-stu-id="23113-104">This article shows you how to migrate an active DNS name to [Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="23113-105">Wanneer u een live site en de DNS-domeinnaam in App Service migreert, is al live verkeer voor de DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="23113-105">When you migrate a live site and its DNS domain name to App Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="23113-106">U kunt uitvaltijd in DNS-omzetting tijdens de migratie vermijden door de naam van de actieve DNS-optie preventief binding aan uw App Service-app.</span><span class="sxs-lookup"><span data-stu-id="23113-106">You can avoid downtime in DNS resolution during the migration by binding the active DNS name to your App Service app preemptively.</span></span>

<span data-ttu-id="23113-107">Als u niet over uitvaltijd in DNS-omzetting vastgesteld, Zie [aangepaste DNS-naam van een bestaande toewijzen aan Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="23113-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23113-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="23113-108">Prerequisites</span></span>

<span data-ttu-id="23113-109">Voltooi deze instructies volgt:</span><span class="sxs-lookup"><span data-stu-id="23113-109">To complete this how-to:</span></span>

- <span data-ttu-id="23113-110">[Zorg ervoor dat uw app in App Service zich niet in de laag gratis](app-service-web-tutorial-custom-domain.md#checkpricing).</span><span class="sxs-lookup"><span data-stu-id="23113-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-the-domain-name-preemptively"></a><span data-ttu-id="23113-111">De domeinnaam optie preventief binden</span><span class="sxs-lookup"><span data-stu-id="23113-111">Bind the domain name preemptively</span></span>

<span data-ttu-id="23113-112">Wanneer u een aangepast domein optie preventief bindt, uitvoeren van de volgende voordat u wijzigingen aanbrengt in de DNS-records:</span><span class="sxs-lookup"><span data-stu-id="23113-112">When you bind a custom domain preemptively, you accomplish both of the following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="23113-113">Domein verifiëren</span><span class="sxs-lookup"><span data-stu-id="23113-113">Verify domain ownership</span></span>
- <span data-ttu-id="23113-114">De domeinnaam voor uw app inschakelen</span><span class="sxs-lookup"><span data-stu-id="23113-114">Enable the domain name for your app</span></span>

<span data-ttu-id="23113-115">Wanneer u ten slotte uw aangepaste DNS-naam van de oude site naar de App Service-app migreert, zal er geen uitvaltijd in DNS-omzetting.</span><span class="sxs-lookup"><span data-stu-id="23113-115">When you finally migrate your custom DNS name from the old site to the App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="23113-116">Domein verificatie-record maken</span><span class="sxs-lookup"><span data-stu-id="23113-116">Create domain verification record</span></span>

<span data-ttu-id="23113-117">Als u wilt verifiëren dat dit domein, een TXT-record toevoegen</span><span class="sxs-lookup"><span data-stu-id="23113-117">To verify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="23113-118">De TXT-record wordt toegewezen uit _awverify.&lt; subdomein >_ naar  _&lt;appname >. azurewebsites.net_.</span><span class="sxs-lookup"><span data-stu-id="23113-118">The TXT record maps from _awverify.&lt;subdomain>_ to _&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="23113-119">De TXT-record dat u nodig hebt, is afhankelijk van de DNS-record dat u wilt migreren.</span><span class="sxs-lookup"><span data-stu-id="23113-119">The TXT record you need depends on the DNS record you want to migrate.</span></span> <span data-ttu-id="23113-120">Zie de volgende tabel voor voorbeelden (`@` vertegenwoordigt doorgaans het hoofddomein):</span><span class="sxs-lookup"><span data-stu-id="23113-120">For examples, see the following table (`@` typically represents the root domain):</span></span>  

| <span data-ttu-id="23113-121">Voorbeeld van DNS-record</span><span class="sxs-lookup"><span data-stu-id="23113-121">DNS record example</span></span> | <span data-ttu-id="23113-122">TXT-Host</span><span class="sxs-lookup"><span data-stu-id="23113-122">TXT Host</span></span> | <span data-ttu-id="23113-123">TXT-waarde</span><span class="sxs-lookup"><span data-stu-id="23113-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="23113-124">@ (root)</span><span class="sxs-lookup"><span data-stu-id="23113-124">@ (root)</span></span> | <span data-ttu-id="23113-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="23113-125">_awverify_</span></span> | <span data-ttu-id="23113-126">_&lt;AppName >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="23113-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="23113-127">www (sub)</span><span class="sxs-lookup"><span data-stu-id="23113-127">www (sub)</span></span> | <span data-ttu-id="23113-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="23113-128">_awverify.www_</span></span> | <span data-ttu-id="23113-129">_&lt;AppName >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="23113-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="23113-130">\*(jokertekens)</span><span class="sxs-lookup"><span data-stu-id="23113-130">\* (wildcard)</span></span> | <span data-ttu-id="23113-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="23113-131">_awverify.\*_</span></span> | <span data-ttu-id="23113-132">_&lt;AppName >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="23113-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="23113-133">Noteer het recordtype van de DNS-naam die u wilt migreren in uw pagina DNS-records.</span><span class="sxs-lookup"><span data-stu-id="23113-133">In your DNS records page, note the record type of the DNS name you want to migrate.</span></span> <span data-ttu-id="23113-134">App Service biedt ondersteuning voor toewijzingen van CNAME- en A-records.</span><span class="sxs-lookup"><span data-stu-id="23113-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-the-domain-for-your-app"></a><span data-ttu-id="23113-135">Het domein voor uw app inschakelen</span><span class="sxs-lookup"><span data-stu-id="23113-135">Enable the domain for your app</span></span>

<span data-ttu-id="23113-136">In de [Azure-portal](https://portal.azure.com), selecteert u in het linkernavigatievenster van de app-pagina **aangepaste domeinen**.</span><span class="sxs-lookup"><span data-stu-id="23113-136">In the [Azure portal](https://portal.azure.com), in the left navigation of the app page, select **Custom domains**.</span></span> 

![Aangepast domein menu](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="23113-138">In de **aangepaste domeinen** pagina de  **+**  pictogram naast **hostnaam toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="23113-138">In the **Custom domains** page, select the **+** icon next to **Add hostname**.</span></span>

![Hostnaam toevoegen](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="23113-140">Typ de volledig gekwalificeerde domeinnaam dat u de TXT-record, zoals toegevoegd `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="23113-140">Type the fully qualified domain name that you added the TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="23113-141">Voor een jokertekendomein (zoals \*. contoso.com), kunt u een DNS-naam die overeenkomt met het jokertekendomein.</span><span class="sxs-lookup"><span data-stu-id="23113-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches the wildcard domain.</span></span> 

<span data-ttu-id="23113-142">Selecteer **valideren**.</span><span class="sxs-lookup"><span data-stu-id="23113-142">Select **Validate**.</span></span>

<span data-ttu-id="23113-143">De **hostnaam toevoegen** knop wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="23113-143">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="23113-144">Zorg ervoor dat **hostnaam recordtype** is ingesteld op het DNS-recordtype dat u wilt migreren.</span><span class="sxs-lookup"><span data-stu-id="23113-144">Make sure that **Hostname record type** is set to the DNS record type you want to migrate.</span></span>

<span data-ttu-id="23113-145">Selecteer **hostnaam toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="23113-145">Select **Add hostname**.</span></span>

![DNS-naam toevoegen aan de app.](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="23113-147">Het kan even duren voor de nieuwe hostnaam worden weergegeven in de app **aangepaste domeinen** pagina.</span><span class="sxs-lookup"><span data-stu-id="23113-147">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="23113-148">Vernieuw de browser voor het bijwerken van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="23113-148">Try refreshing the browser to update the data.</span></span>

![CNAME-record is toegevoegd](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="23113-150">Uw aangepaste DNS-naam is nu ingeschakeld in uw app in Azure.</span><span class="sxs-lookup"><span data-stu-id="23113-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-the-active-dns-name"></a><span data-ttu-id="23113-151">Opnieuw toewijzen van de actieve DNS-naam</span><span class="sxs-lookup"><span data-stu-id="23113-151">Remap the active DNS name</span></span>

<span data-ttu-id="23113-152">De enige nog te doen is opnieuw toewijzen van uw actieve DNS-record om te verwijzen naar App Service.</span><span class="sxs-lookup"><span data-stu-id="23113-152">The only thing left to do is remapping your active DNS record to point to App Service.</span></span> <span data-ttu-id="23113-153">Rechts nu nog steeds verwijst naar de oude site.</span><span class="sxs-lookup"><span data-stu-id="23113-153">Right now, it still points to your old site.</span></span>

<a name="info"></a>

### <a name="copy-the-apps-ip-address-a-record-only"></a><span data-ttu-id="23113-154">Kopiëren van de app IP-adres (alleen een record)</span><span class="sxs-lookup"><span data-stu-id="23113-154">Copy the app's IP address (A record only)</span></span>

<span data-ttu-id="23113-155">Als u opnieuw van een CNAME-record toewijzen, moet u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="23113-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="23113-156">Opnieuw toewijzen van een A-record, moet u de App Service-app externe IP-adres, die wordt weergegeven in de **aangepaste domeinen** pagina.</span><span class="sxs-lookup"><span data-stu-id="23113-156">To remap an A record, you need the App Service app's external IP address, which is shown in the **Custom domains** page.</span></span>

<span data-ttu-id="23113-157">Sluit de **hostnaam toevoegen** pagina door te selecteren **X** in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="23113-157">Close the **Add hostname** page by selecting **X** in the upper-right corner.</span></span> 

<span data-ttu-id="23113-158">In de **aangepaste domeinen** pagina, kopieert u de app IP-adres.</span><span class="sxs-lookup"><span data-stu-id="23113-158">In the **Custom domains** page, copy the app's IP address.</span></span>

![Navigatie naar Azure-app in de portal](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-the-dns-record"></a><span data-ttu-id="23113-160">De DNS-record bijwerken</span><span class="sxs-lookup"><span data-stu-id="23113-160">Update the DNS record</span></span>

<span data-ttu-id="23113-161">Selecteer op de pagina DNS-records van uw domeinprovider de DNS-record opnieuw toewijzen.</span><span class="sxs-lookup"><span data-stu-id="23113-161">Back in the DNS records page of your domain provider, select the DNS record to remap.</span></span>

<span data-ttu-id="23113-162">Voor de `contoso.com` voorbeeld van domein hoofdmap, wijst u de A of CNAME-record zoals de voorbeelden in de volgende tabel:</span><span class="sxs-lookup"><span data-stu-id="23113-162">For the `contoso.com` root domain example, remap the A or CNAME record like the examples in the following table:</span></span> 

| <span data-ttu-id="23113-163">FQDN-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="23113-163">FQDN example</span></span> | <span data-ttu-id="23113-164">Recordtype</span><span class="sxs-lookup"><span data-stu-id="23113-164">Record type</span></span> | <span data-ttu-id="23113-165">Host</span><span class="sxs-lookup"><span data-stu-id="23113-165">Host</span></span> | <span data-ttu-id="23113-166">Waarde</span><span class="sxs-lookup"><span data-stu-id="23113-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="23113-167">Contoso.com (root)</span><span class="sxs-lookup"><span data-stu-id="23113-167">contoso.com (root)</span></span> | <span data-ttu-id="23113-168">A</span><span class="sxs-lookup"><span data-stu-id="23113-168">A</span></span> | `@` | <span data-ttu-id="23113-169">IP-adres uit [kopiëren van de app IP-adres](#info)</span><span class="sxs-lookup"><span data-stu-id="23113-169">IP address from [Copy the app's IP address](#info)</span></span> |
| <span data-ttu-id="23113-170">www.contoso.com (sub)</span><span class="sxs-lookup"><span data-stu-id="23113-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="23113-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="23113-171">CNAME</span></span> | `www` | <span data-ttu-id="23113-172">_&lt;AppName >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="23113-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="23113-173">\*. contoso.com (jokertekens)</span><span class="sxs-lookup"><span data-stu-id="23113-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="23113-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="23113-174">CNAME</span></span> | _\*_ | <span data-ttu-id="23113-175">_&lt;AppName >. azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="23113-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="23113-176">Uw instellingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="23113-176">Save your settings.</span></span>

<span data-ttu-id="23113-177">DNS-query's moeten beginnen met het omzetten van naar uw app in App Service onmiddellijk nadat de DNS-servers gebeurt.</span><span class="sxs-lookup"><span data-stu-id="23113-177">DNS queries should start resolving to your App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23113-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="23113-178">Next steps</span></span>

<span data-ttu-id="23113-179">Ontdek hoe u een aangepaste SSL-certificaat binden aan de App Service.</span><span class="sxs-lookup"><span data-stu-id="23113-179">Learn how to bind a custom SSL certificate to App Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="23113-180">Een bestaande aangepaste SSL-certificaat binden aan Azure-Web-Apps</span><span class="sxs-lookup"><span data-stu-id="23113-180">Bind an existing custom SSL certificate to Azure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
