---
title: aaaAdd een SSL-certificaat tooyour Azure App Service-app | Microsoft Docs
description: Meer informatie over hoe tooadd een SSL-certificaat tooyour App Service-app.
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="b3344-103">Een SSL-certificaat kopen en configureren voor uw Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b3344-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="b3344-104">In deze zelfstudie wordt u uw web-app beveiligen door het aanschaffen van een SSL-certificaat voor uw  **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, veilig opslaan in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), en het koppelen van met een aangepast domein.</span><span class="sxs-lookup"><span data-stu-id="b3344-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-tooazure"></a><span data-ttu-id="b3344-105">Stap 1 - logboek in tooAzure</span><span class="sxs-lookup"><span data-stu-id="b3344-105">Step 1 - Log in tooAzure</span></span>

<span data-ttu-id="b3344-106">Meld u bij toohello Azure-portal op http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="b3344-106">Log in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="b3344-107">Stap 2: een SSL-certificaat bestelling plaatsen</span><span class="sxs-lookup"><span data-stu-id="b3344-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="b3344-108">U kunt een SSL-certificaat-volgorde plaatsen door het maken van een nieuw [App Service-certificaat](https://portal.azure.com/#create/Microsoft.SSL) In Hallo **Azure-portal**.</span><span class="sxs-lookup"><span data-stu-id="b3344-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In hello **Azure portal**.</span></span>

![Maken van het certificaat](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="b3344-110">Voer een beschrijvende **naam** voor uw SSL-certificaat en Voer Hallo **domeinnaam**</span><span class="sxs-lookup"><span data-stu-id="b3344-110">Enter a friendly **Name** for your SSL certificate and enter hello **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="b3344-111">Dit is een van de meest kritieke onderdelen van het aankoopproces Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b3344-111">This is one of hello most critical parts of hello purchase process.</span></span> <span data-ttu-id="b3344-112">Zorg ervoor dat tooenter hostnaam (aangepast domein) dat u wilt dat tooprotect met dit certificaat te corrigeren.</span><span class="sxs-lookup"><span data-stu-id="b3344-112">Make sure tooenter correct host name (custom domain) that you want tooprotect with this certificate.</span></span> <span data-ttu-id="b3344-113">**GEEN** Hallo hostnaam met WWW toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b3344-113">**DO NOT** append hello Host name with WWW.</span></span> 
>

<span data-ttu-id="b3344-114">Selecteer uw **abonnement**, **resourcegroep**, en **SKU van het certificaat**</span><span class="sxs-lookup"><span data-stu-id="b3344-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="b3344-115">App Service Certificate kan alleen worden gebruikt door andere Services App binnen Hallo hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="b3344-115">App Service Certificates can only be used by other App Services within hello same subscription.</span></span>  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a><span data-ttu-id="b3344-116">Stap 3 - Store Hallo certificaat in Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="b3344-116">Step 3 - Store hello certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="b3344-117">[Sleutelkluis](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is een Azure-service die helpt bij het beschermen van de cryptografische sleutels en geheimen beveiligen die door cloudtoepassingen en -services.</span><span class="sxs-lookup"><span data-stu-id="b3344-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="b3344-118">Zodra de Hallo SSL-certificaat aankoop is voltooid, moet u tooopen [App Service Certificate](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource-blade.</span><span class="sxs-lookup"><span data-stu-id="b3344-118">Once hello SSL Certificate purchase is complete, you need tooopen [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![afbeelding van gereed toostore invoegen in KV](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="b3344-120">U ziet dat certificaatstatus **"In behandeling zijnde uitgifte"** omdat er meer stappen moet toocomplete voordat u kunt met dit certificaat.</span><span class="sxs-lookup"><span data-stu-id="b3344-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need toocomplete before you can start using this certificate.</span></span>

<span data-ttu-id="b3344-121">Klik op **Certificaatconfiguratie** in eigenschappen voor certificaat-blade en klik op **stap 1: Store** toostore dit certificaat in Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="b3344-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** toostore this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="b3344-122">Van **Sleutelkluis Status** Blade, klikt u op **Sleutelkluis opslagplaats** toochoose een bestaande Sleutelkluis toostore dit certificaat **of maak nieuwe Sleutelkluis** toocreate nieuwe sleutel kluis binnen hetzelfde abonnement en de resource-groep.</span><span class="sxs-lookup"><span data-stu-id="b3344-122">From **Key Vault Status** Blade, click **Key Vault Repository** toochoose an existing Key Vault toostore this certificate **OR Create New Key Vault** toocreate new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="b3344-123">Azure Sleutelkluis heeft minimale kosten voor het opslaan van dit certificaat.</span><span class="sxs-lookup"><span data-stu-id="b3344-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="b3344-124">Zie voor meer informatie  **[prijsinformatie voor Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.</span><span class="sxs-lookup"><span data-stu-id="b3344-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="b3344-125">Nadat u hebt Hallo Sleutelkluis opslagplaats toostore geselecteerd dit certificaat in, Hallo **Store** optie geslaagd moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b3344-125">Once you have selected hello Key Vault Repository toostore this certificate in, hello **Store** option should show success.</span></span>

![afbeelding van store slagen van KV invoegen](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a><span data-ttu-id="b3344-127">Stap 4 - Hallo domein eigendom verifiëren</span><span class="sxs-lookup"><span data-stu-id="b3344-127">Step 4 - Verify hello Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="b3344-128">Er zijn drie soorten verificatie van het domein wordt ondersteund door App service Certificate: domein, E-mail, handmatige verificatie.</span><span class="sxs-lookup"><span data-stu-id="b3344-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="b3344-129">Deze worden beschreven in meer informatie in Hallo [geavanceerde sectie](#advanced).</span><span class="sxs-lookup"><span data-stu-id="b3344-129">These are explained in more details in hello [Advanced section](#advanced).</span></span>

<span data-ttu-id="b3344-130">Hallo van dezelfde **Certificaatconfiguratie** blade die u in stap 3 gebruikt, klikt u op **stap 2: Controleer of**.</span><span class="sxs-lookup"><span data-stu-id="b3344-130">From hello same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="b3344-131">**Verificatie van domein** dit is de meest geschikte proces Hallo **alleen als** u  **[uw aangepaste domein via Azure App Service hebt aangeschaft.](custom-dns-web-site-buydomains-web-app.md)**</span><span class="sxs-lookup"><span data-stu-id="b3344-131">**Domain Verification** This is hello most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="b3344-132">Klik op **controleren** knop toocomplete deze stap.</span><span class="sxs-lookup"><span data-stu-id="b3344-132">Click on **Verify** button toocomplete this step.</span></span>

![afbeelding van domeinverificatie invoegen](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="b3344-134">Wanneer u op **controleren**, hello gebruiken **vernieuwen** knop tot Hallo **controleren** optie geslaagd moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b3344-134">After clicking **Verify**, use hello **Refresh** button until hello **Verify** option should show success.</span></span>

![afbeelding van INSERT verifiëren in KV](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a><span data-ttu-id="b3344-136">Stap 5: certificaat tooApp Service-App toewijzen</span><span class="sxs-lookup"><span data-stu-id="b3344-136">Step 5 - Assign Certificate tooApp Service App</span></span>

> [!NOTE]
> <span data-ttu-id="b3344-137">Voordat u Hallo stappen in deze sectie, moet een aangepaste domeinnaam hebt gekoppeld aan uw app.</span><span class="sxs-lookup"><span data-stu-id="b3344-137">Before performing hello steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="b3344-138">Zie voor meer informatie  **[configureren van een aangepaste domeinnaam voor een web-app.](app-service-web-tutorial-custom-domain.md)**</span><span class="sxs-lookup"><span data-stu-id="b3344-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="b3344-139">In Hallo  **[Azure-portal](https://portal.azure.com/)**, klikt u op Hallo **App Service** optie op Hallo links van het Hallo-pagina.</span><span class="sxs-lookup"><span data-stu-id="b3344-139">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="b3344-140">Klik op Hallo-naam van uw app toowhich gewenste tooassign dit certificaat.</span><span class="sxs-lookup"><span data-stu-id="b3344-140">Click hello name of your app toowhich you want tooassign this certificate.</span></span>

<span data-ttu-id="b3344-141">In Hallo **instellingen**, klikt u op **SSL-certificaten**.</span><span class="sxs-lookup"><span data-stu-id="b3344-141">In hello **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="b3344-142">Klik op **App Service-certificaat importeren** en selecteer Hallo-certificaat dat u zojuist hebt aangeschaft.</span><span class="sxs-lookup"><span data-stu-id="b3344-142">Click **Import App Service Certificate** and select hello certificate that you just purchased.</span></span>

![afbeelding van het certificaat importeren invoegen](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="b3344-144">In Hallo **ssl-bindingen** sectie Klik op **bindingen toevoegen**, Hallo opgegeven waarin dropdowns tooselect Hallo domain name toosecure gebruiken met SSL en Hallo toouse certificaat.</span><span class="sxs-lookup"><span data-stu-id="b3344-144">In hello **ssl bindings** section Click on **Add bindings**, and use hello dropdowns tooselect hello domain name toosecure with SSL, and hello certificate toouse.</span></span> <span data-ttu-id="b3344-145">U kunt ook selecteren of toouse  **[indicatie voor Server-naam (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  of IP op basis van SSL.</span><span class="sxs-lookup"><span data-stu-id="b3344-145">You may also select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![afbeelding van SSL-bindingen worden ingevoegd](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="b3344-147">Klik op **toevoegen Binding** toosave Hallo wijzigingen en SSL in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="b3344-147">Click **Add Binding** toosave hello changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="b3344-148">Als u hebt geselecteerd **IP SSL gebaseerde** en uw aangepaste domein is geconfigureerd met een A-record, moet u Hallo extra stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b3344-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps.</span></span> <span data-ttu-id="b3344-149">Deze worden beschreven in meer informatie in Hallo [geavanceerde sectie](#Advanced).</span><span class="sxs-lookup"><span data-stu-id="b3344-149">These are explained in more details in hello [Advanced section](#Advanced).</span></span>

<span data-ttu-id="b3344-150">Op dit moment u moet kunnen toovisit uw app met `HTTPS://` in plaats van `HTTP://` tooverify die Hallo certificaat correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="b3344-150">At this point, you should be able toovisit your app using `HTTPS://` instead of `HTTP://` tooverify that hello certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="b3344-151">Stap 6: beheertaken</span><span class="sxs-lookup"><span data-stu-id="b3344-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="b3344-152">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b3344-152">Azure CLI</span></span>

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a><span data-ttu-id="b3344-153">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3344-153">PowerShell</span></span>

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a><span data-ttu-id="b3344-154">Geavanceerd</span><span class="sxs-lookup"><span data-stu-id="b3344-154">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="b3344-155">Domein eigendom verifiëren</span><span class="sxs-lookup"><span data-stu-id="b3344-155">Verifying Domain Ownership</span></span>

<span data-ttu-id="b3344-156">Er zijn twee soorten verificatie van het domein wordt ondersteund door App service Certificate: e-Mail en handmatige verificatie.</span><span class="sxs-lookup"><span data-stu-id="b3344-156">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="b3344-157">Controle e-mail</span><span class="sxs-lookup"><span data-stu-id="b3344-157">Mail Verification</span></span>

<span data-ttu-id="b3344-158">Al is bevestigingsmail verzonden e-mailadres gekoppeld aan dit aangepaste domein toohello.</span><span class="sxs-lookup"><span data-stu-id="b3344-158">Verification email has already been sent toohello Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="b3344-159">toocomplete hello e verificatiestap Hallo e-mail openen en klik op Hallo bevestigingslink.</span><span class="sxs-lookup"><span data-stu-id="b3344-159">toocomplete hello Email verification step, open hello email and click hello verification link.</span></span>

![afbeelding van e-mailverificatie invoegen](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="b3344-161">Als u tooresend Hallo bevestigingsmail nodig hebt, klikt u op Hallo **E-mail opnieuw verzenden** knop.</span><span class="sxs-lookup"><span data-stu-id="b3344-161">If you need tooresend hello verification email, click hello **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="b3344-162">Handmatige verificatie</span><span class="sxs-lookup"><span data-stu-id="b3344-162">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3344-163">HTML-pagina verificatie (werkt alleen met standaard SKU van het certificaat.)</span><span class="sxs-lookup"><span data-stu-id="b3344-163">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="b3344-164">Maken van een HTML-bestand met de naam **'starfield.html'**</span><span class="sxs-lookup"><span data-stu-id="b3344-164">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="b3344-165">Inhoud van dit bestand moet de exacte naam Hallo Hallo domein verificatie Token.</span><span class="sxs-lookup"><span data-stu-id="b3344-165">Content of this file should be hello exact name of hello Domain Verification Token.</span></span> <span data-ttu-id="b3344-166">(U kunt Hallo-token van Hallo domein verificatie Status Blade kopiëren)</span><span class="sxs-lookup"><span data-stu-id="b3344-166">(You can copy hello token from hello Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="b3344-167">Dit bestand in de hoofdmap Hallo van Hallo-webserver die als host fungeert voor uw domein niet uploaden`/.well-known/pki-validation/starfield.html`</span><span class="sxs-lookup"><span data-stu-id="b3344-167">Upload this file at hello root of hello web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="b3344-168">Klik op **vernieuwen** tooupdate Hallo certificaatstatus nadat verificatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b3344-168">Click **Refresh** tooupdate hello certificate status after verification is completed.</span></span> <span data-ttu-id="b3344-169">Het kan enkele minuten duren voordat toocomplete voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="b3344-169">It might take few minutes for verification toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="b3344-170">Controleer of in een terminal met `curl -G http://<domain>/.well-known/pki-validation/starfield.html` antwoord Hallo Hallo moet bevatten `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="b3344-170">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` hello response should contain hello `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="b3344-171">Controle van DNS TXT-Record</span><span class="sxs-lookup"><span data-stu-id="b3344-171">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="b3344-172">Maak een TXT-record met uw DNS-beheer op Hallo `@` subdomein met waarde gelijk toohello domein verificatie Token.</span><span class="sxs-lookup"><span data-stu-id="b3344-172">Using your DNS manager, Create a TXT record on hello `@` subdomain with value equal toohello Domain Verification Token.</span></span>
1. <span data-ttu-id="b3344-173">Klik op **'Vernieuwen'** tooupdate Hallo certificaatstatus nadat verificatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b3344-173">Click **“Refresh”** tooupdate hello Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="b3344-174">U moet een TXT-record toocreate op `@.<domain>` met waarde `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="b3344-174">You need toocreate a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-tooapp-service-app"></a><span data-ttu-id="b3344-175">Toewijzen van certificaat tooApp Service-App</span><span class="sxs-lookup"><span data-stu-id="b3344-175">Assign Certificate tooApp Service App</span></span>

<span data-ttu-id="b3344-176">Als u hebt geselecteerd **IP SSL gebaseerde** en uw aangepaste domein is geconfigureerd met een A-record, moet u Hallo extra stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b3344-176">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps:</span></span>

<span data-ttu-id="b3344-177">Nadat u hebt geconfigureerd SSL-binding op basis van een IP-adres, een vast IP-adres toegewezen tooyour app.</span><span class="sxs-lookup"><span data-stu-id="b3344-177">After you have configured an IP based SSL binding, a dedicated IP address is assigned tooyour app.</span></span> <span data-ttu-id="b3344-178">U kunt dit IP-adres vinden op Hallo **aangepaste domeinen** pagina onder de instellingen van uw app, direct boven Hallo **hostnamen** sectie.</span><span class="sxs-lookup"><span data-stu-id="b3344-178">You can find this IP address on hello **Custom domain** page under settings of your app, right above hello **Hostnames** section.</span></span> <span data-ttu-id="b3344-179">Deze wordt vermeld als **externe IP-adres**</span><span class="sxs-lookup"><span data-stu-id="b3344-179">It is listed as **External IP Address**</span></span>

![afbeelding van IP-SSL invoegen](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="b3344-181">Houd er rekening mee dat dit IP-adres anders is dan het virtuele IP-adres Hallo eerder tooconfigure Hallo A-record voor uw domein gebruikte.</span><span class="sxs-lookup"><span data-stu-id="b3344-181">Note that this IP address is different than hello virtual IP address used previously tooconfigure hello A record for your domain.</span></span> <span data-ttu-id="b3344-182">Als u zijn geconfigureerd toouse SNI op basis van SSL, of zijn niet geconfigureerd toouse SSL, er is geen adres wordt vermeld voor dit item.</span><span class="sxs-lookup"><span data-stu-id="b3344-182">If you are configured toouse SNI based SSL, or are not configured toouse SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="b3344-183">Met de hulpprogramma's geleverd door uw domeinnaamregistrar Hallo Hallo een record voor uw aangepaste domein naam toopoint toohello IP-adres van de vorige stap Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b3344-183">Using hello tools provided by your domain name registrar, modify hello A record for your custom domain name toopoint toohello IP address from hello previous step.</span></span>

## <a name="rekey-and-sync-hello-certificate"></a><span data-ttu-id="b3344-184">Opnieuw genereren van sleutels en Sync Hallo certificaat</span><span class="sxs-lookup"><span data-stu-id="b3344-184">Rekey and Sync hello Certificate</span></span>

<span data-ttu-id="b3344-185">Als u ooit tooRekey uw certificaat moet, selecteert u **sleutel opnieuw genereren en synchroniseren** optie van **certificaateigenschappen** Blade.</span><span class="sxs-lookup"><span data-stu-id="b3344-185">If you ever need tooRekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="b3344-186">Klik op **sleutel opnieuw genereren** knop tooinitiate Hallo proces.</span><span class="sxs-lookup"><span data-stu-id="b3344-186">Click **Rekey** Button tooinitiate hello process.</span></span> <span data-ttu-id="b3344-187">Dit kan toocomplete 1-10 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="b3344-187">This process can take 1-10 minutes toocomplete.</span></span>

![afbeelding van de sleutel opnieuw genereren SSL invoegen](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="b3344-189">Het certificaat opnieuw genereren van sleutels wordt Hallo-certificaat met een nieuw certificaat is uitgegeven door de certificeringsinstantie Hallo getotaliseerd.</span><span class="sxs-lookup"><span data-stu-id="b3344-189">Rekeying your certificate rolls hello certificate with a new certificate issued from hello certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3344-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b3344-190">Next Steps</span></span>

* [<span data-ttu-id="b3344-191">Een Content Delivery Network toevoegen</span><span class="sxs-lookup"><span data-stu-id="b3344-191">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)