---
title: Een bestaande aangepaste SSL-certificaat binden aan Azure Web Apps | Microsoft Docs
description: Hoe u kunt een aangepaste SSL-certificaat binden aan uw web-app, back-end voor mobiele app of API-app in Azure App Service.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 15c31ae5451a31dff2df08047ee43e75edacc127
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-to-azure-web-apps"></a><span data-ttu-id="81899-103">Een bestaande aangepaste SSL-certificaat binden aan Azure-Web-Apps</span><span class="sxs-lookup"><span data-stu-id="81899-103">Bind an existing custom SSL certificate to Azure Web Apps</span></span>

<span data-ttu-id="81899-104">Azure Web Apps biedt een zeer schaalbaar, zelf patch webhosting-service.</span><span class="sxs-lookup"><span data-stu-id="81899-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="81899-105">Deze zelfstudie leert u hoe u kunt een aangepaste SSL-certificaat dat u hebt aangeschaft via een vertrouwde certificeringsinstantie te binden [Azure Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="81899-105">This tutorial shows you how to bind a custom SSL certificate that you purchased from a trusted certificate authority to [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="81899-106">Wanneer u klaar bent, kunt u zult toegang kunnen krijgen tot uw web-app op het HTTPS-eindpunt van uw aangepaste DNS-domein.</span><span class="sxs-lookup"><span data-stu-id="81899-106">When you're finished, you'll be able to access your web app at the HTTPS endpoint of your custom DNS domain.</span></span>

![Web-app met aangepaste SSL-certificaat](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="81899-108">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="81899-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="81899-109">Upgrade van uw app-prijscategorie</span><span class="sxs-lookup"><span data-stu-id="81899-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="81899-110">Uw aangepaste SSL-certificaat binden aan de App Service</span><span class="sxs-lookup"><span data-stu-id="81899-110">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="81899-111">Afdwingen van HTTPS voor uw app</span><span class="sxs-lookup"><span data-stu-id="81899-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="81899-112">SSL-certificaat-binding met scripts automatiseren</span><span class="sxs-lookup"><span data-stu-id="81899-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="81899-113">Als u nodig hebt om een aangepaste SSL-certificaat te verkrijgen, kunt u een in de Azure portal rechtstreeks ophalen en bindt dit aan uw web-app.</span><span class="sxs-lookup"><span data-stu-id="81899-113">If you need to get a custom SSL certificate, you can get one in the Azure portal directly and bind it to your web app.</span></span> <span data-ttu-id="81899-114">Ga als volgt de [App Service Certificate zelfstudie](web-sites-purchase-ssl-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="81899-114">Follow the [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81899-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="81899-115">Prerequisites</span></span>

<span data-ttu-id="81899-116">Vereisten voor het voltooien van deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="81899-116">To complete this tutorial:</span></span>

- [<span data-ttu-id="81899-117">Een App Service-app maken</span><span class="sxs-lookup"><span data-stu-id="81899-117">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="81899-118">Een aangepaste DNS-naam toegewezen aan uw web-app</span><span class="sxs-lookup"><span data-stu-id="81899-118">Map a custom DNS name to your web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="81899-119">Een SSL-certificaat van een vertrouwde certificeringsinstantie verkrijgen</span><span class="sxs-lookup"><span data-stu-id="81899-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="81899-120">Vereisten voor SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="81899-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="81899-121">Als u een certificaat in App Service, kan het certificaat moet voldoen aan de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="81899-121">To use a certificate in App Service, the certificate must meet all the following requirements:</span></span>

* <span data-ttu-id="81899-122">Ondertekend door een vertrouwde certificeringsinstantie</span><span class="sxs-lookup"><span data-stu-id="81899-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="81899-123">Geëxporteerd als een PFX-wachtwoord is beveiligd bestand</span><span class="sxs-lookup"><span data-stu-id="81899-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="81899-124">Persoonlijke sleutel van minstens 2048 bits bevat lang</span><span class="sxs-lookup"><span data-stu-id="81899-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="81899-125">Bevat alle tussenliggende certificaten in de certificaatketen</span><span class="sxs-lookup"><span data-stu-id="81899-125">Contains all intermediate certificates in the certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="81899-126">**Elliptic Curve Cryptography (ECC)-certificaten** kunt werken met App Service, maar worden niet behandeld in dit artikel wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="81899-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="81899-127">Werken met uw certificeringsinstantie op de exacte stappen voor het maken van ECC-certificaten.</span><span class="sxs-lookup"><span data-stu-id="81899-127">Work with your certificate authority on the exact steps to create ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="81899-128">Voorbereiden van uw web-app</span><span class="sxs-lookup"><span data-stu-id="81899-128">Prepare your web app</span></span>

<span data-ttu-id="81899-129">Een aangepaste SSL-certificaat binden aan uw web-app uw [App Service-abonnement](https://azure.microsoft.com/pricing/details/app-service/) moet zich in de **Basic**, **standaard**, of **Premium** laag.</span><span class="sxs-lookup"><span data-stu-id="81899-129">To bind a custom SSL certificate to your web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in the **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="81899-130">In deze stap maakt ervoor u zorgen dat uw web-app is in de ondersteunde prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="81899-130">In this step, you make sure that your web app is in the supported pricing tier.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="81899-131">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="81899-131">Log in to Azure</span></span>

<span data-ttu-id="81899-132">Open de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="81899-132">Open the [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-to-your-web-app"></a><span data-ttu-id="81899-133">Navigeer naar uw web-app</span><span class="sxs-lookup"><span data-stu-id="81899-133">Navigate to your web app</span></span>

<span data-ttu-id="81899-134">Klik in het menu links op **App Services**, en klik vervolgens op de naam van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="81899-134">From the left menu, click **App Services**, and then click the name of your web app.</span></span>

![Web-app selecteren](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="81899-136">U bevindt zich op de beheerpagina van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="81899-136">You have landed in the management page of your web app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="81899-137">Controleer de prijscategorie</span><span class="sxs-lookup"><span data-stu-id="81899-137">Check the pricing tier</span></span>

<span data-ttu-id="81899-138">Schuif in de linkernavigatiebalk van uw web-app-pagina naar de **instellingen** sectie en selecteer **opschalen (App Service-abonnement)**.</span><span class="sxs-lookup"><span data-stu-id="81899-138">In the left-hand navigation of your web app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Omhoog schalen-menu](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="81899-140">Controleer of uw web-app is niet in de **vrije** of **gedeelde** laag.</span><span class="sxs-lookup"><span data-stu-id="81899-140">Check to make sure that your web app is not in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="81899-141">De huidige tier uw web-app is gemarkeerd met een donker blauw vak.</span><span class="sxs-lookup"><span data-stu-id="81899-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![Controleer de prijscategorie](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="81899-143">Aangepaste SSL wordt niet ondersteund in de **vrije** of **gedeelde** laag.</span><span class="sxs-lookup"><span data-stu-id="81899-143">Custom SSL is not supported in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="81899-144">Als u moet worden uitgebreid, volgt u de stappen in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="81899-144">If you need to scale up, follow the steps in the next section.</span></span> <span data-ttu-id="81899-145">Anders sluit de **Kies uw prijscategorie** pagina en doorgaan met [uploaden en de SSL-certificaat binden](#upload).</span><span class="sxs-lookup"><span data-stu-id="81899-145">Otherwise, close the **Choose your pricing tier** page and skip to [Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="81899-146">Uw App Service-abonnement opschalen</span><span class="sxs-lookup"><span data-stu-id="81899-146">Scale up your App Service plan</span></span>

<span data-ttu-id="81899-147">Selecteer een van de **Basic**, **standaard**, of **Premium** lagen.</span><span class="sxs-lookup"><span data-stu-id="81899-147">Select one of the **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="81899-148">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="81899-148">Click **Select**.</span></span>

![Kies de prijscategorie](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="81899-150">Wanneer u de volgende melding ziet, is de schaalbewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="81899-150">When you see the following notification, the scale operation is complete.</span></span>

![Melding opschalen](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="81899-152">SSL-certificaat binden</span><span class="sxs-lookup"><span data-stu-id="81899-152">Bind your SSL certificate</span></span>

<span data-ttu-id="81899-153">U bent klaar om uw SSL-certificaat uploaden naar uw web-app.</span><span class="sxs-lookup"><span data-stu-id="81899-153">You are ready to upload your SSL certificate to your web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="81899-154">Tussenliggende certificaten samenvoegen</span><span class="sxs-lookup"><span data-stu-id="81899-154">Merge intermediate certificates</span></span>

<span data-ttu-id="81899-155">Als uw certificeringsinstantie meerdere certificaten in de certificaatketen geeft, moet u de certificaten in de volgorde samenvoegen.</span><span class="sxs-lookup"><span data-stu-id="81899-155">If your certificate authority gives you multiple certificates in the certificate chain, you need to merge the certificates in order.</span></span> 

<span data-ttu-id="81899-156">U doet dit door elk certificaat dat u hebt ontvangen in een teksteditor te openen.</span><span class="sxs-lookup"><span data-stu-id="81899-156">To do this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="81899-157">Maak een bestand voor het samengevoegde certificaat, aangeroepen _mergedcertificate.crt_.</span><span class="sxs-lookup"><span data-stu-id="81899-157">Create a file for the merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="81899-158">Kopieer de inhoud van elk certificaat in dit bestand in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="81899-158">In a text editor, copy the content of each certificate into this file.</span></span> <span data-ttu-id="81899-159">De volgorde van uw certificaten moet eruitzien als in de volgende sjabloon:</span><span class="sxs-lookup"><span data-stu-id="81899-159">The order of your certificates should look like the following template:</span></span>

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-to-pfx"></a><span data-ttu-id="81899-160">PFX-certificaat exporteren</span><span class="sxs-lookup"><span data-stu-id="81899-160">Export certificate to PFX</span></span>

<span data-ttu-id="81899-161">Exporteer uw samengevoegde SSL-certificaat met de persoonlijke sleutel die uw certificaataanvraag is gegenereerd met.</span><span class="sxs-lookup"><span data-stu-id="81899-161">Export your merged SSL certificate with the private key that your certificate request was generated with.</span></span>

<span data-ttu-id="81899-162">Als u de certificaataanvraag met het OpenSSL gegenereerd, kunt u een bestand met een persoonlijke sleutel hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="81899-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="81899-163">Voer de volgende opdracht om uw certificaat exporteren naar PFX.</span><span class="sxs-lookup"><span data-stu-id="81899-163">To export your certificate to PFX, run the following command.</span></span> <span data-ttu-id="81899-164">Vervang de tijdelijke aanduidingen  _&lt;persoonlijke sleutelbestand >_ en  _&lt;samengevoegd--certificaatbestand >_.</span><span class="sxs-lookup"><span data-stu-id="81899-164">Replace the placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="81899-165">Wanneer u wordt gevraagd, moet u een wachtwoord voor export definiëren.</span><span class="sxs-lookup"><span data-stu-id="81899-165">When prompted, define an export password.</span></span> <span data-ttu-id="81899-166">U hebt dit wachtwoord gebruiken wanneer u later uw SSL-certificaat uploadt naar App Service.</span><span class="sxs-lookup"><span data-stu-id="81899-166">You'll use this password when uploading your SSL certificate to App Service later.</span></span>

<span data-ttu-id="81899-167">Als u IIS gebruikt of _Certreq.exe_ bij het genereren van uw certificaataanvraag, installeer het certificaat in uw lokale computer en vervolgens [Exporteer het certificaat naar PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="81899-167">If you used IIS or _Certreq.exe_ to generate your certificate request, install the certificate to your local machine, and then [export the certificate to PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="81899-168">Uw SSL-certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="81899-168">Upload your SSL certificate</span></span>

<span data-ttu-id="81899-169">Als u wilt uw SSL-certificaat uploaden, klikt u op **SSL-certificaten** in het linkernavigatievenster van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="81899-169">To upload your SSL certificate, click **SSL certificates** in the left navigation of your web app.</span></span>

<span data-ttu-id="81899-170">Klik op **-certificaat uploaden**.</span><span class="sxs-lookup"><span data-stu-id="81899-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="81899-171">In **PFX-certificaatbestand**, selecteer uw PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="81899-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="81899-172">In **certificaatwachtwoord**, typ het wachtwoord dat u hebt gemaakt toen u het PFX-bestand hebt geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="81899-172">In **Certificate password**, type the password that you created when you exported the PFX file.</span></span>

<span data-ttu-id="81899-173">Klik op **Uploaden**.</span><span class="sxs-lookup"><span data-stu-id="81899-173">Click **Upload**.</span></span>

![Certificaat uploaden](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="81899-175">Wanneer de App Service klaar is met uw certificaat uploaden, wordt deze weergegeven de **SSL-certificaten** pagina.</span><span class="sxs-lookup"><span data-stu-id="81899-175">When App Service finishes uploading your certificate, it appears in the **SSL certificates** page.</span></span>

![Certificaat geüpload](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="81899-177">SSL-certificaat binden</span><span class="sxs-lookup"><span data-stu-id="81899-177">Bind your SSL certificate</span></span>

<span data-ttu-id="81899-178">In de **SSL-bindingen** sectie, klikt u op **binding toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="81899-178">In the **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="81899-179">In de **SSL-Binding toevoegen** pagina, gebruikt u de vervolgkeuzelijsten selecteren voor het beveiligen van de naam van het domein en het certificaat te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="81899-179">In the **Add SSL Binding** page, use the dropdowns to select the domain name to secure, and the certificate to use.</span></span>

> [!NOTE]
> <span data-ttu-id="81899-180">Als u uw certificaat hebt geüpload, maar niet ziet de domein-/-namen in de **hostnaam** dropdown, probeer de browserpagina te vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="81899-180">If you have uploaded your certificate but don't see the domain name(s) in the **Hostname** dropdown, try refreshing the browser page.</span></span>
>
>

<span data-ttu-id="81899-181">In **SSL Type**, opgeven of  **[indicatie voor Server-naam (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  of SSL op basis van IP.</span><span class="sxs-lookup"><span data-stu-id="81899-181">In **SSL Type**, select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="81899-182">**Op basis van SNI SSL** -op basis van meerdere SNI SSL-bindingen kunnen worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="81899-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="81899-183">Deze optie kunt meerdere SSL-certificaten voor het beveiligen van meerdere domeinen op hetzelfde IP-adres.</span><span class="sxs-lookup"><span data-stu-id="81899-183">This option allows multiple SSL certificates to secure multiple domains on the same IP address.</span></span> <span data-ttu-id="81899-184">De meeste moderne browsers (met inbegrip van Internet Explorer, Chrome, Firefox en Opera) ondersteuning voor SNI (vinden uitgebreidere browser ondersteuningsinformatie op [Servernaamindicatie](http://wikipedia.org/wiki/Server_Name_Indication)).</span><span class="sxs-lookup"><span data-stu-id="81899-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="81899-185">**IP-gebaseerde SSL** -slechts één IP-gebaseerde SSL-binding kan worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="81899-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="81899-186">Deze optie kan slechts één SSL-certificaat voor het beveiligen van een specifieke openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="81899-186">This option allows only one SSL certificate to secure a dedicated public IP address.</span></span> <span data-ttu-id="81899-187">Als u wilt beveiligen in meerdere domeinen, moet u beveiligen ze allemaal zijn gebaseerd op het SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="81899-187">To secure multiple domains, you must secure them all using the same SSL certificate.</span></span> <span data-ttu-id="81899-188">Dit is de traditionele optie voor SSL-binding.</span><span class="sxs-lookup"><span data-stu-id="81899-188">This is the traditional option for SSL binding.</span></span>

<span data-ttu-id="81899-189">Klik op **Binding toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="81899-189">Click **Add Binding**.</span></span>

![SSL-certificaat binden](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="81899-191">Wanneer de App Service klaar is met uw certificaat uploaden, wordt deze weergegeven de **SSL-bindingen** secties.</span><span class="sxs-lookup"><span data-stu-id="81899-191">When App Service finishes uploading your certificate, it appears in the **SSL bindings** sections.</span></span>

![Certificaat dat is gebonden aan web-app](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="81899-193">Opnieuw toewijzen van een record voor IP-SSL</span><span class="sxs-lookup"><span data-stu-id="81899-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="81899-194">Als u geen IP-gebaseerde SSL in uw web-app gebruikt, gaat u naar [Test HTTPS voor uw aangepaste domein](#test).</span><span class="sxs-lookup"><span data-stu-id="81899-194">If you don't use IP-based SSL in your web app, skip to [Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="81899-195">Uw web-app maakt standaard gebruik van een gedeelde openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="81899-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="81899-196">Wanneer u een certificaat met SSL op basis van IP verbonden, wordt een nieuwe, toegewezen IP-adres voor uw web-app in App Service gemaakt.</span><span class="sxs-lookup"><span data-stu-id="81899-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="81899-197">Als u een A-record hebt toegewezen aan uw web-app, bijwerken van uw domein register met dit nieuwe, toegewezen IP-adres.</span><span class="sxs-lookup"><span data-stu-id="81899-197">If you have mapped an A record to your web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="81899-198">Uw web-app **aangepaste domeinen** pagina wordt bijgewerkt met de nieuwe, toegewezen IP-adres.</span><span class="sxs-lookup"><span data-stu-id="81899-198">Your web app's **Custom domain** page is updated with the new, dedicated IP address.</span></span> <span data-ttu-id="81899-199">[Kopieer dit IP-adres](app-service-web-tutorial-custom-domain.md#info), klikt u vervolgens [opnieuw toewijzen van de A-record](app-service-web-tutorial-custom-domain.md#map-an-a-record) naar deze nieuwe IP-adres.</span><span class="sxs-lookup"><span data-stu-id="81899-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap the A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) to this new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="81899-200">Test HTTPS</span><span class="sxs-lookup"><span data-stu-id="81899-200">Test HTTPS</span></span>

<span data-ttu-id="81899-201">Alle die nog moet doen nu om ervoor te zorgen dat HTTPS voor uw aangepaste domein werkt is.</span><span class="sxs-lookup"><span data-stu-id="81899-201">All that's left to do now is to make sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="81899-202">Blader in verschillende browsers naar `https://<your.custom.domain>` om te zien dat het fungeert van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="81899-202">In various browsers, browse to `https://<your.custom.domain>` to see that it serves up your web app.</span></span>

![Navigatie naar Azure-app in de portal](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="81899-204">Als uw web-app biedt u validatiefouten van het certificaat, gebruikt u waarschijnlijk een zelfondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="81899-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="81899-205">Als dit niet het geval is, mogelijk hebt u weggelaten tussenliggende certificaten als u uw certificaat naar het PFX-bestand exporteert.</span><span class="sxs-lookup"><span data-stu-id="81899-205">If that's not the case, you may have left out intermediate certificates when you export your certificate to the PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="81899-206">HTTPS afdwingen</span><span class="sxs-lookup"><span data-stu-id="81899-206">Enforce HTTPS</span></span>

<span data-ttu-id="81899-207">App Service biedt *niet* afdwingen HTTPS, zodat iedereen nog steeds toegang tot uw web-app met behulp van HTTP.</span><span class="sxs-lookup"><span data-stu-id="81899-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="81899-208">Als u wilt afdwingen HTTPS voor uw web-app, definieert u een regel herschrijven in de _web.config_ -bestand voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="81899-208">To enforce HTTPS for your web app, define a rewrite rule in the _web.config_ file for your web app.</span></span> <span data-ttu-id="81899-209">App Service maakt gebruik van dit bestand, ongeacht het kader van de taal van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="81899-209">App Service uses this file, regardless of the language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="81899-210">Er is een specifieke taal zijn gebonden omleiding van aanvragen.</span><span class="sxs-lookup"><span data-stu-id="81899-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="81899-211">ASP.NET MVC kunt gebruiken de [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter in plaats van de regel herschrijven in _web.config_.</span><span class="sxs-lookup"><span data-stu-id="81899-211">ASP.NET MVC can use the [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of the rewrite rule in _web.config_.</span></span>

<span data-ttu-id="81899-212">Als u een .NET-ontwikkelaar bent, moet u relatief vertrouwd zijn met dit bestand zijn.</span><span class="sxs-lookup"><span data-stu-id="81899-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="81899-213">Het is in de hoofdmap van uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="81899-213">It is in the root of your solution.</span></span>

<span data-ttu-id="81899-214">U kunt ook als u met PHP, Node.js, Python of Java ontwikkelt, is er een kans we dit bestand namens jou gegenereerd in App Service.</span><span class="sxs-lookup"><span data-stu-id="81899-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="81899-215">Verbinding maken met uw web-app FTP-eindpunt volgens de instructies op [uw app implementeren in Azure App Service met behulp van FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="81899-215">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="81899-216">Dit bestand moet zich in _/home/site/wwwroot_.</span><span class="sxs-lookup"><span data-stu-id="81899-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="81899-217">Als dit niet het geval is, maakt u een _web.config_ bestand in deze map met de volgende XML-code:</span><span class="sxs-lookup"><span data-stu-id="81899-217">If not, create a _web.config_ file in this folder with the following XML:</span></span>

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

<span data-ttu-id="81899-218">Voor een bestaande _web.config_ bestand, Kopieer de gehele `<rule>` element in uw _web.config_van `configuration/system.webServer/rewrite/rules` element.</span><span class="sxs-lookup"><span data-stu-id="81899-218">For an existing _web.config_ file, copy the entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="81899-219">Als er andere `<rule>` elementen in uw _web.config_, plaatst u de gekopieerde `<rule>` element voordat de andere `<rule>` elementen.</span><span class="sxs-lookup"><span data-stu-id="81899-219">If there are other `<rule>` elements in your _web.config_, place the copied `<rule>` element before the other `<rule>` elements.</span></span>

<span data-ttu-id="81899-220">Deze regel retourneert HTTP 301 (permanente omleiding) en het HTTPS-protocol, wanneer de gebruiker een HTTP-aanvraag aan uw web-app maakt.</span><span class="sxs-lookup"><span data-stu-id="81899-220">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="81899-221">Bijvoorbeeld, wordt hij omgeleid van `http://contoso.com` naar `https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="81899-221">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

<span data-ttu-id="81899-222">Zie voor meer informatie over de module voor het herschrijven van IIS-URL, de [herschrijven van URL's](http://www.iis.net/downloads/microsoft/url-rewrite) documentatie.</span><span class="sxs-lookup"><span data-stu-id="81899-222">For more information on the IIS URL Rewrite module, see the [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="81899-223">Afdwingen van HTTPS voor Web-Apps op Linux</span><span class="sxs-lookup"><span data-stu-id="81899-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="81899-224">Op Linux-App Service biedt *niet* afdwingen HTTPS, zodat iedereen nog steeds toegang tot uw web-app met behulp van HTTP.</span><span class="sxs-lookup"><span data-stu-id="81899-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="81899-225">Als u wilt afdwingen HTTPS voor uw web-app, definieert u een regel herschrijven in de _.htaccess_ -bestand voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="81899-225">To enforce HTTPS for your web app, define a rewrite rule in the _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="81899-226">Verbinding maken met uw web-app FTP-eindpunt volgens de instructies op [uw app implementeren in Azure App Service met behulp van FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="81899-226">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="81899-227">In _/home/site/wwwroot_, maak een _.htaccess_ bestand met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="81899-227">In _/home/site/wwwroot_, create an _.htaccess_ file with the following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="81899-228">Deze regel retourneert HTTP 301 (permanente omleiding) en het HTTPS-protocol, wanneer de gebruiker een HTTP-aanvraag aan uw web-app maakt.</span><span class="sxs-lookup"><span data-stu-id="81899-228">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="81899-229">Bijvoorbeeld, wordt hij omgeleid van `http://contoso.com` naar `https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="81899-229">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="81899-230">Automatiseren met behulp van scripts</span><span class="sxs-lookup"><span data-stu-id="81899-230">Automate with scripts</span></span>

<span data-ttu-id="81899-231">U kunt SSL-bindingen automatiseren voor uw web-app met behulp van scripts, met behulp van de [Azure CLI](/cli/azure/install-azure-cli) of [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="81899-231">You can automate SSL bindings for your web app with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="81899-232">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="81899-232">Azure CLI</span></span>

<span data-ttu-id="81899-233">De volgende opdracht een geëxporteerde PFX-bestand uploadt en de vingerafdruk van het opgehaald.</span><span class="sxs-lookup"><span data-stu-id="81899-233">The following command uploads an exported PFX file and gets the thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="81899-234">De volgende opdracht voegt een SNI op basis van een SSL-binding met de vingerafdruk van de vorige opdracht.</span><span class="sxs-lookup"><span data-stu-id="81899-234">The following command adds an SNI-based SSL binding, using the thumbprint from the previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="81899-235">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="81899-235">Azure PowerShell</span></span>

<span data-ttu-id="81899-236">De volgende opdracht een geëxporteerde PFX-bestand uploadt en voegt een SNI op basis van een SSL-binding.</span><span class="sxs-lookup"><span data-stu-id="81899-236">The following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="81899-237">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="81899-237">Next steps</span></span>

<span data-ttu-id="81899-238">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="81899-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="81899-239">Upgrade van uw app-prijscategorie</span><span class="sxs-lookup"><span data-stu-id="81899-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="81899-240">Uw aangepaste SSL-certificaat binden aan de App Service</span><span class="sxs-lookup"><span data-stu-id="81899-240">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="81899-241">Afdwingen van HTTPS voor uw app</span><span class="sxs-lookup"><span data-stu-id="81899-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="81899-242">SSL-certificaat-binding met scripts automatiseren</span><span class="sxs-lookup"><span data-stu-id="81899-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="81899-243">Ga naar de volgende zelfstudie voor meer informatie over het gebruik van Azure Content Delivery Network.</span><span class="sxs-lookup"><span data-stu-id="81899-243">Advance to the next tutorial to learn how to use Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="81899-244">Een Content Delivery Network (CDN) toevoegen aan een Azure App Service</span><span class="sxs-lookup"><span data-stu-id="81899-244">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)
