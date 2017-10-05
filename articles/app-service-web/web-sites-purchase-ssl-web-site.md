---
title: Een SSL-certificaat toevoegen aan uw app in Azure App Service | Microsoft Docs
description: Informatie over het toevoegen van een SSL-certificaat aan uw App Service-app.
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
ms.openlocfilehash: 191dd7240ad15b4936a72bc27a2d0162350f3afb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="24ee7-103">Een SSL-certificaat kopen en configureren voor uw Azure App Service</span><span class="sxs-lookup"><span data-stu-id="24ee7-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="24ee7-104">In deze zelfstudie wordt u uw web-app beveiligen door het aanschaffen van een SSL-certificaat voor uw  **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, veilig opslaan in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), en het koppelen van met een aangepast domein.</span><span class="sxs-lookup"><span data-stu-id="24ee7-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-to-azure"></a><span data-ttu-id="24ee7-105">Stap 1 - logboek in naar Azure</span><span class="sxs-lookup"><span data-stu-id="24ee7-105">Step 1 - Log in to Azure</span></span>

<span data-ttu-id="24ee7-106">Aanmelden bij de Azure portal op http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="24ee7-106">Log in to the Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="24ee7-107">Stap 2: een SSL-certificaat bestelling plaatsen</span><span class="sxs-lookup"><span data-stu-id="24ee7-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="24ee7-108">U kunt een SSL-certificaat-volgorde plaatsen door het maken van een nieuw [App Service-certificaat](https://portal.azure.com/#create/Microsoft.SSL) In de **Azure-portal**.</span><span class="sxs-lookup"><span data-stu-id="24ee7-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In the **Azure portal**.</span></span>

![Maken van het certificaat](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="24ee7-110">Voer een beschrijvende **naam** voor uw SSL-certificaat en voer de **domeinnaam**</span><span class="sxs-lookup"><span data-stu-id="24ee7-110">Enter a friendly **Name** for your SSL certificate and enter the **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="24ee7-111">Dit is een van de belangrijkste onderdelen van het aankoopproces.</span><span class="sxs-lookup"><span data-stu-id="24ee7-111">This is one of the most critical parts of the purchase process.</span></span> <span data-ttu-id="24ee7-112">Zorg ervoor dat juiste host-naam (aangepaste domein) die u wilt beveiligen met dit certificaat op te geven.</span><span class="sxs-lookup"><span data-stu-id="24ee7-112">Make sure to enter correct host name (custom domain) that you want to protect with this certificate.</span></span> <span data-ttu-id="24ee7-113">**GEEN** de hostnaam met WWW toevoegen.</span><span class="sxs-lookup"><span data-stu-id="24ee7-113">**DO NOT** append the Host name with WWW.</span></span> 
>

<span data-ttu-id="24ee7-114">Selecteer uw **abonnement**, **resourcegroep**, en **SKU van het certificaat**</span><span class="sxs-lookup"><span data-stu-id="24ee7-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="24ee7-115">App Service-certificaten kunnen alleen worden gebruikt door andere Services App binnen hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="24ee7-115">App Service Certificates can only be used by other App Services within the same subscription.</span></span>  
>

## <a name="step-3---store-the-certificate-in-azure-key-vault"></a><span data-ttu-id="24ee7-116">Stap 3: het certificaat wordt opgeslagen in Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="24ee7-116">Step 3 - Store the certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="24ee7-117">[Sleutelkluis](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is een Azure-service die helpt bij het beschermen van de cryptografische sleutels en geheimen beveiligen die door cloudtoepassingen en -services.</span><span class="sxs-lookup"><span data-stu-id="24ee7-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="24ee7-118">Zodra de aankoop van het SSL-certificaat voltooid is, moet u openen [App Service Certificate](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource-blade.</span><span class="sxs-lookup"><span data-stu-id="24ee7-118">Once the SSL Certificate purchase is complete, you need to open [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![afbeelding van gereed is om op te slaan in KV invoegen](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="24ee7-120">U ziet dat certificaatstatus **"In behandeling zijnde uitgifte"** omdat er meer stappen u uitvoeren moet voordat u met dit certificaat kunt gaan.</span><span class="sxs-lookup"><span data-stu-id="24ee7-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need to complete before you can start using this certificate.</span></span>

<span data-ttu-id="24ee7-121">Klik op **Certificaatconfiguratie** in eigenschappen voor certificaat-blade en klik op **stap 1: opslaan** dit certificaat wordt opgeslagen in Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="24ee7-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** to store this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="24ee7-122">Van **Sleutelkluis Status** Blade, klikt u op **Sleutelkluis opslagplaats** kiezen een bestaande Sleutelkluis voor het opslaan van dit certificaat **of maak nieuwe Sleutelkluis** voor het maken van nieuwe Sleutelkluis binnen hetzelfde abonnement en de resource-groep.</span><span class="sxs-lookup"><span data-stu-id="24ee7-122">From **Key Vault Status** Blade, click **Key Vault Repository** to choose an existing Key Vault to store this certificate **OR Create New Key Vault** to create new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="24ee7-123">Azure Sleutelkluis heeft minimale kosten voor het opslaan van dit certificaat.</span><span class="sxs-lookup"><span data-stu-id="24ee7-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="24ee7-124">Zie voor meer informatie  **[prijsinformatie voor Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.</span><span class="sxs-lookup"><span data-stu-id="24ee7-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="24ee7-125">Nadat u de opslagplaats van de kluis sleutel voor het opslaan van dit certificaat, hebt geselecteerd de **opslaan** optie geslaagd moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="24ee7-125">Once you have selected the Key Vault Repository to store this certificate in, the **Store** option should show success.</span></span>

![afbeelding van store slagen van KV invoegen](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-the-domain-ownership"></a><span data-ttu-id="24ee7-127">Stap 4: Controleer of het eigendom van het domein</span><span class="sxs-lookup"><span data-stu-id="24ee7-127">Step 4 - Verify the Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="24ee7-128">Er zijn drie soorten verificatie van het domein wordt ondersteund door App service Certificate: domein, E-mail, handmatige verificatie.</span><span class="sxs-lookup"><span data-stu-id="24ee7-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="24ee7-129">Deze worden beschreven in meer informatie in de [geavanceerde sectie](#advanced).</span><span class="sxs-lookup"><span data-stu-id="24ee7-129">These are explained in more details in the [Advanced section](#advanced).</span></span>

<span data-ttu-id="24ee7-130">Uit dezelfde **Certificaatconfiguratie** blade die u in stap 3 gebruikt, klikt u op **stap 2: Controleer of**.</span><span class="sxs-lookup"><span data-stu-id="24ee7-130">From the same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="24ee7-131">**Verificatie van domein** dit is het meest geschikte proces **alleen als** u  **[uw aangepaste domein via Azure App Service hebt aangeschaft.](custom-dns-web-site-buydomains-web-app.md)**</span><span class="sxs-lookup"><span data-stu-id="24ee7-131">**Domain Verification** This is the most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="24ee7-132">Klik op **controleren** knop om deze stap te voltooien.</span><span class="sxs-lookup"><span data-stu-id="24ee7-132">Click on **Verify** button to complete this step.</span></span>

![afbeelding van domeinverificatie invoegen](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="24ee7-134">Wanneer u op **controleren**, gebruiken de **vernieuwen** knop totdat de **controleren** optie geslaagd moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="24ee7-134">After clicking **Verify**, use the **Refresh** button until the **Verify** option should show success.</span></span>

![afbeelding van INSERT verifiëren in KV](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-to-app-service-app"></a><span data-ttu-id="24ee7-136">Stap 5 - certificaat toewijzen aan de App Service-App</span><span class="sxs-lookup"><span data-stu-id="24ee7-136">Step 5 - Assign Certificate to App Service App</span></span>

> [!NOTE]
> <span data-ttu-id="24ee7-137">Voordat u de stappen in deze sectie, moet een aangepaste domeinnaam hebt gekoppeld aan uw app.</span><span class="sxs-lookup"><span data-stu-id="24ee7-137">Before performing the steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="24ee7-138">Zie voor meer informatie  **[configureren van een aangepaste domeinnaam voor een web-app.](app-service-web-tutorial-custom-domain.md)**</span><span class="sxs-lookup"><span data-stu-id="24ee7-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="24ee7-139">In de  **[Azure-portal](https://portal.azure.com/)**, klikt u op de **App Service** optie aan de linkerkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="24ee7-139">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span></span>

<span data-ttu-id="24ee7-140">Klik op de naam van uw app waaraan u dit certificaat wilt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="24ee7-140">Click the name of your app to which you want to assign this certificate.</span></span>

<span data-ttu-id="24ee7-141">In de **instellingen**, klikt u op **SSL-certificaten**.</span><span class="sxs-lookup"><span data-stu-id="24ee7-141">In the **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="24ee7-142">Klik op **App Service-certificaat importeren** en selecteer het certificaat dat u zojuist hebt aangeschaft.</span><span class="sxs-lookup"><span data-stu-id="24ee7-142">Click **Import App Service Certificate** and select the certificate that you just purchased.</span></span>

![afbeelding van het certificaat importeren invoegen](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="24ee7-144">In de **ssl-bindingen** sectie Klik op **bindingen toevoegen**, en selecteer de naam van het domein te beveiligen met SSL en het certificaat te gebruiken met de vervolgkeuzelijsten.</span><span class="sxs-lookup"><span data-stu-id="24ee7-144">In the **ssl bindings** section Click on **Add bindings**, and use the dropdowns to select the domain name to secure with SSL, and the certificate to use.</span></span> <span data-ttu-id="24ee7-145">U kunt ook selecteren of u wilt gebruiken  **[indicatie voor Server-naam (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  of IP op basis van SSL.</span><span class="sxs-lookup"><span data-stu-id="24ee7-145">You may also select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![afbeelding van SSL-bindingen worden ingevoegd](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="24ee7-147">Klik op **toevoegen Binding** de wijzigingen opslaan en SSL in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="24ee7-147">Click **Add Binding** to save the changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="24ee7-148">Als u hebt geselecteerd **IP SSL gebaseerde** en uw aangepaste domein is geconfigureerd met een A-record, moet u de volgende aanvullende stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="24ee7-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps.</span></span> <span data-ttu-id="24ee7-149">Deze worden beschreven in meer informatie in de [geavanceerde sectie](#Advanced).</span><span class="sxs-lookup"><span data-stu-id="24ee7-149">These are explained in more details in the [Advanced section](#Advanced).</span></span>

<span data-ttu-id="24ee7-150">Op dit moment moet u kunnen bezoeken uw app met `HTTPS://` in plaats van `HTTP://` om te controleren of het certificaat correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="24ee7-150">At this point, you should be able to visit your app using `HTTPS://` instead of `HTTP://` to verify that the certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="24ee7-151">Stap 6: beheertaken</span><span class="sxs-lookup"><span data-stu-id="24ee7-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="24ee7-152">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="24ee7-152">Azure CLI</span></span>

<span data-ttu-id="24ee7-153">[!code-azurecli[belangrijkste](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "een aangepaste SSL-certificaat binden aan een web-app")]</span><span class="sxs-lookup"><span data-stu-id="24ee7-153">[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span> 

### <a name="powershell"></a><span data-ttu-id="24ee7-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="24ee7-154">PowerShell</span></span>

<span data-ttu-id="24ee7-155">[!code-powershell[belangrijkste](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "een aangepaste SSL-certificaat binden aan een web-app")]</span><span class="sxs-lookup"><span data-stu-id="24ee7-155">[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]</span></span>

## <a name="advanced"></a><span data-ttu-id="24ee7-156">Geavanceerd</span><span class="sxs-lookup"><span data-stu-id="24ee7-156">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="24ee7-157">Domein eigendom verifiëren</span><span class="sxs-lookup"><span data-stu-id="24ee7-157">Verifying Domain Ownership</span></span>

<span data-ttu-id="24ee7-158">Er zijn twee soorten verificatie van het domein wordt ondersteund door App service Certificate: e-Mail en handmatige verificatie.</span><span class="sxs-lookup"><span data-stu-id="24ee7-158">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="24ee7-159">Controle e-mail</span><span class="sxs-lookup"><span data-stu-id="24ee7-159">Mail Verification</span></span>

<span data-ttu-id="24ee7-160">Reeds is bevestigingsmail verzonden naar de e-adressen die zijn gekoppeld aan dit aangepast domein.</span><span class="sxs-lookup"><span data-stu-id="24ee7-160">Verification email has already been sent to the Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="24ee7-161">De e-verificatiestap voltooid, opent u het e-mailbericht en klik op de koppeling voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="24ee7-161">To complete the Email verification step, open the email and click the verification link.</span></span>

![afbeelding van e-mailverificatie invoegen](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="24ee7-163">Als u de verificatie-e-mail verzenden moet, klikt u op de **E-mail opnieuw verzenden** knop.</span><span class="sxs-lookup"><span data-stu-id="24ee7-163">If you need to resend the verification email, click the **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="24ee7-164">Handmatige verificatie</span><span class="sxs-lookup"><span data-stu-id="24ee7-164">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24ee7-165">HTML-pagina verificatie (werkt alleen met standaard SKU van het certificaat.)</span><span class="sxs-lookup"><span data-stu-id="24ee7-165">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="24ee7-166">Maken van een HTML-bestand met de naam **'starfield.html'**</span><span class="sxs-lookup"><span data-stu-id="24ee7-166">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="24ee7-167">Inhoud van dit bestand moet de exacte naam van het domein verificatie-Token.</span><span class="sxs-lookup"><span data-stu-id="24ee7-167">Content of this file should be the exact name of the Domain Verification Token.</span></span> <span data-ttu-id="24ee7-168">(U kunt het token van de Blade domein verificatie Status kopiëren)</span><span class="sxs-lookup"><span data-stu-id="24ee7-168">(You can copy the token from the Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="24ee7-169">Dit bestand in de hoofdmap van de webserver die als host fungeert voor uw domein niet uploaden`/.well-known/pki-validation/starfield.html`</span><span class="sxs-lookup"><span data-stu-id="24ee7-169">Upload this file at the root of the web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="24ee7-170">Klik op **vernieuwen** wilt bijwerken van de certificaatstatus nadat de verificatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="24ee7-170">Click **Refresh** to update the certificate status after verification is completed.</span></span> <span data-ttu-id="24ee7-171">Het duurt enkele minuten voor verificatie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="24ee7-171">It might take few minutes for verification to complete.</span></span>

> [!TIP]
> <span data-ttu-id="24ee7-172">Controleer of in een terminal met `curl -G http://<domain>/.well-known/pki-validation/starfield.html` het antwoord moet bevatten de `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="24ee7-172">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` the response should contain the `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="24ee7-173">Controle van DNS TXT-Record</span><span class="sxs-lookup"><span data-stu-id="24ee7-173">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="24ee7-174">Maak een TXT-record met uw DNS-beheer op de `@` subdomein met waarde gelijk is aan het domein verificatie-Token.</span><span class="sxs-lookup"><span data-stu-id="24ee7-174">Using your DNS manager, Create a TXT record on the `@` subdomain with value equal to the Domain Verification Token.</span></span>
1. <span data-ttu-id="24ee7-175">Klik op **'Vernieuwen'** de certificaatstatus bijwerken nadat de verificatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="24ee7-175">Click **“Refresh”** to update the Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="24ee7-176">U moet een TXT-record maken op `@.<domain>` met waarde `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="24ee7-176">You need to create a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-to-app-service-app"></a><span data-ttu-id="24ee7-177">Certificaat toewijzen aan App Service-App</span><span class="sxs-lookup"><span data-stu-id="24ee7-177">Assign Certificate to App Service App</span></span>

<span data-ttu-id="24ee7-178">Als u hebt geselecteerd **IP SSL gebaseerde** en uw aangepaste domein is geconfigureerd met een A-record, moet u de volgende aanvullende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="24ee7-178">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps:</span></span>

<span data-ttu-id="24ee7-179">Nadat u hebt geconfigureerd SSL-binding op basis van een IP-adres, een vast IP-adres is toegewezen aan uw app.</span><span class="sxs-lookup"><span data-stu-id="24ee7-179">After you have configured an IP based SSL binding, a dedicated IP address is assigned to your app.</span></span> <span data-ttu-id="24ee7-180">U kunt dit IP-adres vinden op de **aangepaste domeinen** pagina onder de instellingen van uw app, direct boven de **hostnamen** sectie.</span><span class="sxs-lookup"><span data-stu-id="24ee7-180">You can find this IP address on the **Custom domain** page under settings of your app, right above the **Hostnames** section.</span></span> <span data-ttu-id="24ee7-181">Deze wordt vermeld als **externe IP-adres**</span><span class="sxs-lookup"><span data-stu-id="24ee7-181">It is listed as **External IP Address**</span></span>

![afbeelding van IP-SSL invoegen](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="24ee7-183">Houd er rekening mee dat dit IP-adres afwijkt van het virtuele IP-adres is eerder gebruikt voor het configureren van de A-record voor uw domein.</span><span class="sxs-lookup"><span data-stu-id="24ee7-183">Note that this IP address is different than the virtual IP address used previously to configure the A record for your domain.</span></span> <span data-ttu-id="24ee7-184">Als u zijn geconfigureerd voor gebruik SNI op basis van SSL, of zijn niet geconfigureerd om SSL te gebruiken, geen adres wordt vermeld voor dit item.</span><span class="sxs-lookup"><span data-stu-id="24ee7-184">If you are configured to use SNI based SSL, or are not configured to use SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="24ee7-185">Met de hulpprogramma's door uw domeinnaamregistrar, wijzig de A-record voor uw aangepaste domeinnaam om te verwijzen naar het IP-adres van de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="24ee7-185">Using the tools provided by your domain name registrar, modify the A record for your custom domain name to point to the IP address from the previous step.</span></span>

## <a name="rekey-and-sync-the-certificate"></a><span data-ttu-id="24ee7-186">Sleutel opnieuw genereren en synchroniseren van het certificaat</span><span class="sxs-lookup"><span data-stu-id="24ee7-186">Rekey and Sync the Certificate</span></span>

<span data-ttu-id="24ee7-187">Als u ooit sleutel opnieuw genereren van uw certificaat wilt, selecteert u **sleutel opnieuw genereren en synchroniseren** optie van **certificaateigenschappen** Blade.</span><span class="sxs-lookup"><span data-stu-id="24ee7-187">If you ever need to Rekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="24ee7-188">Klik op **sleutel opnieuw genereren** om het proces te starten.</span><span class="sxs-lookup"><span data-stu-id="24ee7-188">Click **Rekey** Button to initiate the process.</span></span> <span data-ttu-id="24ee7-189">Dit kan 1 tot 10 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="24ee7-189">This process can take 1-10 minutes to complete.</span></span>

![afbeelding van de sleutel opnieuw genereren SSL invoegen](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="24ee7-191">Het certificaat opnieuw genereren van sleutels, wordt het certificaat met een nieuw certificaat is uitgegeven door de certificeringsinstantie.</span><span class="sxs-lookup"><span data-stu-id="24ee7-191">Rekeying your certificate rolls the certificate with a new certificate issued from the certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24ee7-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="24ee7-192">Next Steps</span></span>

* [<span data-ttu-id="24ee7-193">Een Content Delivery Network toevoegen</span><span class="sxs-lookup"><span data-stu-id="24ee7-193">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)