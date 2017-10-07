---
title: aaaBind een bestaande aangepaste SSL-certificaat tooAzure Web-Apps | Microsoft Docs
description: Meer informatie over tootoobind een aangepaste SSL-certificaat tooyour web-app, back-end voor mobiele app of API-app in Azure App Service.
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
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a><span data-ttu-id="7ea4e-103">Binden van een bestaande aangepaste SSL-certificaat tooAzure Web-Apps</span><span class="sxs-lookup"><span data-stu-id="7ea4e-103">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>

<span data-ttu-id="7ea4e-104">Azure Web Apps biedt een zeer schaalbaar, zelf patch webhosting-service.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="7ea4e-105">Deze zelfstudie laat zien hoe toobind een aangepaste SSL-certificaat die u hebt aangeschaft via een vertrouwde certificeringsinstantie te[Azure Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7ea4e-105">This tutorial shows you how toobind a custom SSL certificate that you purchased from a trusted certificate authority too[Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="7ea4e-106">Wanneer u klaar bent, moet u kunnen tooaccess uw web-app op Hallo HTTPS-eindpunt van uw aangepaste DNS-domein.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-106">When you're finished, you'll be able tooaccess your web app at hello HTTPS endpoint of your custom DNS domain.</span></span>

![Web-app met aangepaste SSL-certificaat](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="7ea4e-108">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="7ea4e-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7ea4e-109">Upgrade van uw app-prijscategorie</span><span class="sxs-lookup"><span data-stu-id="7ea4e-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="7ea4e-110">Uw aangepaste SSL-certificaat tooApp Service binden</span><span class="sxs-lookup"><span data-stu-id="7ea4e-110">Bind your custom SSL certificate tooApp Service</span></span>
> * <span data-ttu-id="7ea4e-111">Afdwingen van HTTPS voor uw app</span><span class="sxs-lookup"><span data-stu-id="7ea4e-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="7ea4e-112">SSL-certificaat-binding met scripts automatiseren</span><span class="sxs-lookup"><span data-stu-id="7ea4e-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="7ea4e-113">Als u een aangepaste SSL-certificaat tooget nodig, kunt u één in hello Azure-portal rechtstreeks ophalen en bindt dit tooyour web-app.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-113">If you need tooget a custom SSL certificate, you can get one in hello Azure portal directly and bind it tooyour web app.</span></span> <span data-ttu-id="7ea4e-114">Ga als volgt Hallo [App Service Certificate zelfstudie](web-sites-purchase-ssl-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="7ea4e-114">Follow hello [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ea4e-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7ea4e-115">Prerequisites</span></span>

<span data-ttu-id="7ea4e-116">toocomplete in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="7ea4e-116">toocomplete this tutorial:</span></span>

- [<span data-ttu-id="7ea4e-117">Een App Service-app maken</span><span class="sxs-lookup"><span data-stu-id="7ea4e-117">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="7ea4e-118">Toewijzen van een aangepaste DNS-naam tooyour web-app</span><span class="sxs-lookup"><span data-stu-id="7ea4e-118">Map a custom DNS name tooyour web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="7ea4e-119">Een SSL-certificaat van een vertrouwde certificeringsinstantie verkrijgen</span><span class="sxs-lookup"><span data-stu-id="7ea4e-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="7ea4e-120">Vereisten voor SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="7ea4e-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="7ea4e-121">een certificaat in App Service toouse, Hallo certificaat moet voldoen aan alle Hallo volgens de vereisten:</span><span class="sxs-lookup"><span data-stu-id="7ea4e-121">toouse a certificate in App Service, hello certificate must meet all hello following requirements:</span></span>

* <span data-ttu-id="7ea4e-122">Ondertekend door een vertrouwde certificeringsinstantie</span><span class="sxs-lookup"><span data-stu-id="7ea4e-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="7ea4e-123">Geëxporteerd als een PFX-wachtwoord is beveiligd bestand</span><span class="sxs-lookup"><span data-stu-id="7ea4e-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="7ea4e-124">Persoonlijke sleutel van minstens 2048 bits bevat lang</span><span class="sxs-lookup"><span data-stu-id="7ea4e-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="7ea4e-125">Bevat alle tussenliggende certificaten in de certificaatketen Hallo</span><span class="sxs-lookup"><span data-stu-id="7ea4e-125">Contains all intermediate certificates in hello certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="7ea4e-126">**Elliptic Curve Cryptography (ECC)-certificaten** kunt werken met App Service, maar worden niet behandeld in dit artikel wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="7ea4e-127">Werken met uw certificeringsinstantie op Hallo exacte stappen toocreate ECC-certificaten.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-127">Work with your certificate authority on hello exact steps toocreate ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="7ea4e-128">Voorbereiden van uw web-app</span><span class="sxs-lookup"><span data-stu-id="7ea4e-128">Prepare your web app</span></span>

<span data-ttu-id="7ea4e-129">toobind een aangepaste SSL-certificaat tooyour web-app, uw [App Service-abonnement](https://azure.microsoft.com/pricing/details/app-service/) moet Hallo **Basic**, **standaard**, of **Premium** laag.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-129">toobind a custom SSL certificate tooyour web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in hello **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="7ea4e-130">In deze stap maakt ervoor u zorgen dat uw web-app wordt in Hallo ondersteund prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-130">In this step, you make sure that your web app is in hello supported pricing tier.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="7ea4e-131">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="7ea4e-131">Log in tooAzure</span></span>

<span data-ttu-id="7ea4e-132">Open Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7ea4e-132">Open hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-tooyour-web-app"></a><span data-ttu-id="7ea4e-133">Navigeer tooyour web-app</span><span class="sxs-lookup"><span data-stu-id="7ea4e-133">Navigate tooyour web app</span></span>

<span data-ttu-id="7ea4e-134">In het linkermenu hello, klikt u op **App Services**, en klik vervolgens op Hallo-naam van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-134">From hello left menu, click **App Services**, and then click hello name of your web app.</span></span>

![Web-app selecteren](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="7ea4e-136">U bevindt zich in de pagina voor het beheren van uw web-app Hallo.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-136">You have landed in hello management page of your web app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="7ea4e-137">Hallo prijscategorie controleren</span><span class="sxs-lookup"><span data-stu-id="7ea4e-137">Check hello pricing tier</span></span>

<span data-ttu-id="7ea4e-138">Schuif in de linkernavigatiebalk Hallo van uw app webpagina toohello **instellingen** sectie en selecteer **opschalen (App Service-abonnement)**.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-138">In hello left-hand navigation of your web app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Omhoog schalen-menu](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="7ea4e-140">Controleer toomake ervoor dat uw web-app niet wordt Hallo **vrije** of **gedeelde** laag.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-140">Check toomake sure that your web app is not in hello **Free** or **Shared** tier.</span></span> <span data-ttu-id="7ea4e-141">De huidige tier uw web-app is gemarkeerd met een donker blauw vak.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![Controleer de prijscategorie](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="7ea4e-143">Aangepaste SSL wordt niet ondersteund in Hallo **vrije** of **gedeelde** laag.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-143">Custom SSL is not supported in hello **Free** or **Shared** tier.</span></span> <span data-ttu-id="7ea4e-144">Als u nodig hebt tooscale, stappen Hallo in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-144">If you need tooscale up, follow hello steps in hello next section.</span></span> <span data-ttu-id="7ea4e-145">Anders sluit Hallo **Kies uw prijscategorie** pagina en te overslaan[uploaden en de SSL-certificaat binden](#upload).</span><span class="sxs-lookup"><span data-stu-id="7ea4e-145">Otherwise, close hello **Choose your pricing tier** page and skip too[Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="7ea4e-146">Uw App Service-abonnement opschalen</span><span class="sxs-lookup"><span data-stu-id="7ea4e-146">Scale up your App Service plan</span></span>

<span data-ttu-id="7ea4e-147">Selecteer een van de Hallo **Basic**, **standaard**, of **Premium** lagen.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-147">Select one of hello **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="7ea4e-148">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-148">Click **Select**.</span></span>

![Kies de prijscategorie](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="7ea4e-150">Wanneer u de volgende kennisgeving Hallo ziet, is Hallo schaalbewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-150">When you see hello following notification, hello scale operation is complete.</span></span>

![Melding opschalen](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="7ea4e-152">SSL-certificaat binden</span><span class="sxs-lookup"><span data-stu-id="7ea4e-152">Bind your SSL certificate</span></span>

<span data-ttu-id="7ea4e-153">U gereed tooupload zijn uw SSL-certificaat tooyour web-app.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-153">You are ready tooupload your SSL certificate tooyour web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="7ea4e-154">Tussenliggende certificaten samenvoegen</span><span class="sxs-lookup"><span data-stu-id="7ea4e-154">Merge intermediate certificates</span></span>

<span data-ttu-id="7ea4e-155">Als uw certificeringsinstantie meerdere certificaten in de certificaatketen hello geeft, moet u toomerge Hallo certificaten in de volgorde.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-155">If your certificate authority gives you multiple certificates in hello certificate chain, you need toomerge hello certificates in order.</span></span> 

<span data-ttu-id="7ea4e-156">toodo moet dit open elk certificaat u hebt ontvangen in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-156">toodo this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="7ea4e-157">Maak een bestand voor Hallo Samengevoegde certificaat, genaamd _mergedcertificate.crt_.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-157">Create a file for hello merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="7ea4e-158">Kopieer Hallo inhoud van elk certificaat in dit bestand in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-158">In a text editor, copy hello content of each certificate into this file.</span></span> <span data-ttu-id="7ea4e-159">Hallo-volgorde van uw certificaten moet eruitzien als Hallo sjabloon te volgen:</span><span class="sxs-lookup"><span data-stu-id="7ea4e-159">hello order of your certificates should look like hello following template:</span></span>

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

### <a name="export-certificate-toopfx"></a><span data-ttu-id="7ea4e-160">TooPFX certificaat exporteren</span><span class="sxs-lookup"><span data-stu-id="7ea4e-160">Export certificate tooPFX</span></span>

<span data-ttu-id="7ea4e-161">Uw samengevoegde SSL-certificaat met persoonlijke sleutel Hallo die uw certificaataanvraag is gegenereerd met exporteren.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-161">Export your merged SSL certificate with hello private key that your certificate request was generated with.</span></span>

<span data-ttu-id="7ea4e-162">Als u de certificaataanvraag met het OpenSSL gegenereerd, kunt u een bestand met een persoonlijke sleutel hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="7ea4e-163">tooexport uw certificaat tooPFX, Hallo volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-163">tooexport your certificate tooPFX, run hello following command.</span></span> <span data-ttu-id="7ea4e-164">Vervang de tijdelijke aanduidingen Hallo  _&lt;persoonlijke sleutelbestand >_ en  _&lt;samengevoegd--certificaatbestand >_.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-164">Replace hello placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="7ea4e-165">Wanneer u wordt gevraagd, moet u een wachtwoord voor export definiëren.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-165">When prompted, define an export password.</span></span> <span data-ttu-id="7ea4e-166">U hebt dit wachtwoord gebruiken tijdens het uploaden van uw SSL-certificaat tooApp Service later.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-166">You'll use this password when uploading your SSL certificate tooApp Service later.</span></span>

<span data-ttu-id="7ea4e-167">Als u IIS gebruikt of _Certreq.exe_ toogenerate uw certificaataanvraag, installatie Hallo certificaat tooyour lokale computer, en vervolgens [exporteren Hallo certificaat tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="7ea4e-167">If you used IIS or _Certreq.exe_ toogenerate your certificate request, install hello certificate tooyour local machine, and then [export hello certificate tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="7ea4e-168">Uw SSL-certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="7ea4e-168">Upload your SSL certificate</span></span>

<span data-ttu-id="7ea4e-169">tooupload uw SSL-certificaat, klik op **SSL-certificaten** in Hallo linkernavigatiebalk van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-169">tooupload your SSL certificate, click **SSL certificates** in hello left navigation of your web app.</span></span>

<span data-ttu-id="7ea4e-170">Klik op **-certificaat uploaden**.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="7ea4e-171">In **PFX-certificaatbestand**, selecteer uw PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="7ea4e-172">In **certificaatwachtwoord**, type Hallo wachtwoord die u hebt gemaakt tijdens het exporteren van Hallo PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-172">In **Certificate password**, type hello password that you created when you exported hello PFX file.</span></span>

<span data-ttu-id="7ea4e-173">Klik op **Uploaden**.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-173">Click **Upload**.</span></span>

![Certificaat uploaden](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="7ea4e-175">Wanneer de App Service klaar is met uw certificaat uploaden, wordt deze in Hallo **SSL-certificaten** pagina.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-175">When App Service finishes uploading your certificate, it appears in hello **SSL certificates** page.</span></span>

![Certificaat geüpload](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="7ea4e-177">SSL-certificaat binden</span><span class="sxs-lookup"><span data-stu-id="7ea4e-177">Bind your SSL certificate</span></span>

<span data-ttu-id="7ea4e-178">In Hallo **SSL-bindingen** sectie, klikt u op **binding toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-178">In hello **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="7ea4e-179">In Hallo **SSL-Binding toevoegen** pagina, Hallo opgegeven waarin dropdowns tooselect Hallo domain name toosecure en Hallo certificaat toouse gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-179">In hello **Add SSL Binding** page, use hello dropdowns tooselect hello domain name toosecure, and hello certificate toouse.</span></span>

> [!NOTE]
> <span data-ttu-id="7ea4e-180">Als u uw certificaat hebt geüpload, maar niet Hallo domein /-namen in Hallo ziet **hostnaam** vervolgkeuzelijst probeer Hallo browserpagina te vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-180">If you have uploaded your certificate but don't see hello domain name(s) in hello **Hostname** dropdown, try refreshing hello browser page.</span></span>
>
>

<span data-ttu-id="7ea4e-181">In **SSL Type**, selecteer of toouse  **[indicatie voor Server-naam (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  of SSL op basis van IP.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-181">In **SSL Type**, select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="7ea4e-182">**Op basis van SNI SSL** -op basis van meerdere SNI SSL-bindingen kunnen worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="7ea4e-183">Met deze optie kunt u meerdere SSL-certificaten toosecure meerdere domeinen op Hallo hetzelfde IP-adres.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-183">This option allows multiple SSL certificates toosecure multiple domains on hello same IP address.</span></span> <span data-ttu-id="7ea4e-184">De meeste moderne browsers (met inbegrip van Internet Explorer, Chrome, Firefox en Opera) ondersteuning voor SNI (vinden uitgebreidere browser ondersteuningsinformatie op [Servernaamindicatie](http://wikipedia.org/wiki/Server_Name_Indication)).</span><span class="sxs-lookup"><span data-stu-id="7ea4e-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="7ea4e-185">**IP-gebaseerde SSL** -slechts één IP-gebaseerde SSL-binding kan worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="7ea4e-186">Deze optie kan slechts één SSL-certificaat toosecure een specifieke openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-186">This option allows only one SSL certificate toosecure a dedicated public IP address.</span></span> <span data-ttu-id="7ea4e-187">toosecure meerdere domeinen, kunt u beveiligen door ze met behulp van alle Hallo SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-187">toosecure multiple domains, you must secure them all using hello same SSL certificate.</span></span> <span data-ttu-id="7ea4e-188">Dit is de traditionele optie Hallo voor SSL-binding.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-188">This is hello traditional option for SSL binding.</span></span>

<span data-ttu-id="7ea4e-189">Klik op **Binding toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-189">Click **Add Binding**.</span></span>

![SSL-certificaat binden](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="7ea4e-191">Wanneer de App Service klaar is met uw certificaat uploaden, wordt deze in Hallo **SSL-bindingen** secties.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-191">When App Service finishes uploading your certificate, it appears in hello **SSL bindings** sections.</span></span>

![Certificaat gebonden tooweb app](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="7ea4e-193">Opnieuw toewijzen van een record voor IP-SSL</span><span class="sxs-lookup"><span data-stu-id="7ea4e-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="7ea4e-194">Als u geen IP-gebaseerde SSL in uw web-app gebruikt, gaat u verder te[Test HTTPS voor uw aangepaste domein](#test).</span><span class="sxs-lookup"><span data-stu-id="7ea4e-194">If you don't use IP-based SSL in your web app, skip too[Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="7ea4e-195">Uw web-app maakt standaard gebruik van een gedeelde openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="7ea4e-196">Wanneer u een certificaat met SSL op basis van IP verbonden, wordt een nieuwe, toegewezen IP-adres voor uw web-app in App Service gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="7ea4e-197">Als u een A-record tooyour-web-app hebt gekoppeld, bijwerken van uw domein register met dit nieuwe, toegewezen IP-adres.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-197">If you have mapped an A record tooyour web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="7ea4e-198">Uw web-app **aangepaste domeinen** pagina met Hallo nieuwe, toegewezen IP-adres wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-198">Your web app's **Custom domain** page is updated with hello new, dedicated IP address.</span></span> <span data-ttu-id="7ea4e-199">[Kopieer dit IP-adres](app-service-web-tutorial-custom-domain.md#info), klikt u vervolgens [opnieuw toewijzen Hallo een record](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis nieuwe IP-adres.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap hello A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="7ea4e-200">Test HTTPS</span><span class="sxs-lookup"><span data-stu-id="7ea4e-200">Test HTTPS</span></span>

<span data-ttu-id="7ea4e-201">Alles wat toodo nu is verdwenen toomake ervoor dat HTTPS voor uw aangepaste domein werkt is.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-201">All that's left toodo now is toomake sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="7ea4e-202">In verschillende browsers te bladeren`https://<your.custom.domain>` toosee die het van uw web-app fungeert.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-202">In various browsers, browse too`https://<your.custom.domain>` toosee that it serves up your web app.</span></span>

![Navigatie in de portal tooAzure app](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="7ea4e-204">Als uw web-app biedt u validatiefouten van het certificaat, gebruikt u waarschijnlijk een zelfondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="7ea4e-205">Als dat niet Hallo geval is, mogelijk hebt u weggelaten tussenliggende certificaten wanneer u uw certificaat toohello PFX-bestand exporteren.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-205">If that's not hello case, you may have left out intermediate certificates when you export your certificate toohello PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="7ea4e-206">HTTPS afdwingen</span><span class="sxs-lookup"><span data-stu-id="7ea4e-206">Enforce HTTPS</span></span>

<span data-ttu-id="7ea4e-207">App Service biedt *niet* afdwingen HTTPS, zodat iedereen nog steeds toegang tot uw web-app met behulp van HTTP.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="7ea4e-208">tooenforce HTTPS voor uw web-app definiëren een regel herschrijven in Hallo _web.config_ -bestand voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-208">tooenforce HTTPS for your web app, define a rewrite rule in hello _web.config_ file for your web app.</span></span> <span data-ttu-id="7ea4e-209">App Service maakt gebruik van dit bestand, ongeacht de taalframework Hallo van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-209">App Service uses this file, regardless of hello language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="7ea4e-210">Er is een specifieke taal zijn gebonden omleiding van aanvragen.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="7ea4e-211">ASP.NET MVC kunt Hallo [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter in plaats van de regel voor het herschrijven van Hallo in _web.config_.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-211">ASP.NET MVC can use hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of hello rewrite rule in _web.config_.</span></span>

<span data-ttu-id="7ea4e-212">Als u een .NET-ontwikkelaar bent, moet u relatief vertrouwd zijn met dit bestand zijn.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="7ea4e-213">Het is in de hoofdmap Hallo van uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-213">It is in hello root of your solution.</span></span>

<span data-ttu-id="7ea4e-214">U kunt ook als u met PHP, Node.js, Python of Java ontwikkelt, is er een kans we dit bestand namens jou gegenereerd in App Service.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="7ea4e-215">Verbinding maken met tooyour van web-app FTP-eindpunt met behulp Hallo-instructies in [implementeren van uw app tooAzure App Service met behulp van FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="7ea4e-215">Connect tooyour web app's FTP endpoint by following hello instructions at [Deploy your app tooAzure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="7ea4e-216">Dit bestand moet zich in _/home/site/wwwroot_.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="7ea4e-217">Als dit niet het geval is, maakt u een _web.config_ bestand in deze map Hello XML te volgen:</span><span class="sxs-lookup"><span data-stu-id="7ea4e-217">If not, create a _web.config_ file in this folder with hello following XML:</span></span>

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

<span data-ttu-id="7ea4e-218">Voor een bestaande _web.config_ bestand, Hallo gehele kopiëren `<rule>` element in uw _web.config_van `configuration/system.webServer/rewrite/rules` element.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-218">For an existing _web.config_ file, copy hello entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="7ea4e-219">Als er andere `<rule>` elementen in uw _web.config_, plaats Hallo gekopieerd `<rule>` element voordat andere Hallo `<rule>` elementen.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-219">If there are other `<rule>` elements in your _web.config_, place hello copied `<rule>` element before hello other `<rule>` elements.</span></span>

<span data-ttu-id="7ea4e-220">Deze regel wordt een HTTP 301 (permanente omleiding) toohello HTTPS-protocol wanneer Hallo gebruiker een HTTP-aanvraag tooyour web-app maakt.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-220">This rule returns an HTTP 301 (permanent redirect) toohello HTTPS protocol whenever hello user makes an HTTP request tooyour web app.</span></span> <span data-ttu-id="7ea4e-221">Bijvoorbeeld, wordt hij omgeleid van `http://contoso.com` te`https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-221">For example, it redirects from `http://contoso.com` too`https://contoso.com`.</span></span>

<span data-ttu-id="7ea4e-222">Zie voor meer informatie over Hallo herschrijven van IIS URL's module Hallo [herschrijven van URL's](http://www.iis.net/downloads/microsoft/url-rewrite) documentatie.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-222">For more information on hello IIS URL Rewrite module, see hello [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="7ea4e-223">Afdwingen van HTTPS voor Web-Apps op Linux</span><span class="sxs-lookup"><span data-stu-id="7ea4e-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="7ea4e-224">Op Linux-App Service biedt *niet* afdwingen HTTPS, zodat iedereen nog steeds toegang tot uw web-app met behulp van HTTP.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="7ea4e-225">tooenforce HTTPS voor uw web-app definiëren een regel herschrijven in Hallo _.htaccess_ -bestand voor uw web-app.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-225">tooenforce HTTPS for your web app, define a rewrite rule in hello _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="7ea4e-226">Verbinding maken met tooyour van web-app FTP-eindpunt met behulp Hallo-instructies in [implementeren van uw app tooAzure App Service met behulp van FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="7ea4e-226">Connect tooyour web app's FTP endpoint by following hello instructions at [Deploy your app tooAzure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="7ea4e-227">In _/home/site/wwwroot_, maak een _.htaccess_ bestand met de volgende code Hallo:</span><span class="sxs-lookup"><span data-stu-id="7ea4e-227">In _/home/site/wwwroot_, create an _.htaccess_ file with hello following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="7ea4e-228">Deze regel wordt een HTTP 301 (permanente omleiding) toohello HTTPS-protocol wanneer Hallo gebruiker een HTTP-aanvraag tooyour web-app maakt.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-228">This rule returns an HTTP 301 (permanent redirect) toohello HTTPS protocol whenever hello user makes an HTTP request tooyour web app.</span></span> <span data-ttu-id="7ea4e-229">Bijvoorbeeld, wordt hij omgeleid van `http://contoso.com` te`https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-229">For example, it redirects from `http://contoso.com` too`https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="7ea4e-230">Automatiseren met behulp van scripts</span><span class="sxs-lookup"><span data-stu-id="7ea4e-230">Automate with scripts</span></span>

<span data-ttu-id="7ea4e-231">U kunt SSL-bindingen automatiseren voor uw web-app met behulp van scripts, met behulp van Hallo [Azure CLI](/cli/azure/install-azure-cli) of [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7ea4e-231">You can automate SSL bindings for your web app with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="7ea4e-232">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7ea4e-232">Azure CLI</span></span>

<span data-ttu-id="7ea4e-233">Hallo na de opdracht een geëxporteerde PFX-bestand uploadt en Hallo vingerafdruk opgehaald.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-233">hello following command uploads an exported PFX file and gets hello thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="7ea4e-234">Hallo voegt volgende opdracht een SNI op basis van een SSL-binding, met de vingerafdruk van het Hallo uit de vorige opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-234">hello following command adds an SNI-based SSL binding, using hello thumbprint from hello previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="7ea4e-235">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ea4e-235">Azure PowerShell</span></span>

<span data-ttu-id="7ea4e-236">Hallo volgende opdracht een geëxporteerde PFX-bestand uploadt en voegt een SNI op basis van een SSL-binding.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-236">hello following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="7ea4e-237">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7ea4e-237">Next steps</span></span>

<span data-ttu-id="7ea4e-238">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="7ea4e-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7ea4e-239">Upgrade van uw app-prijscategorie</span><span class="sxs-lookup"><span data-stu-id="7ea4e-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="7ea4e-240">Uw aangepaste SSL-certificaat tooApp Service binden</span><span class="sxs-lookup"><span data-stu-id="7ea4e-240">Bind your custom SSL certificate tooApp Service</span></span>
> * <span data-ttu-id="7ea4e-241">Afdwingen van HTTPS voor uw app</span><span class="sxs-lookup"><span data-stu-id="7ea4e-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="7ea4e-242">SSL-certificaat-binding met scripts automatiseren</span><span class="sxs-lookup"><span data-stu-id="7ea4e-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="7ea4e-243">Hoe gaan van de volgende zelfstudie toolearn toohello toouse Azure Content Delivery Network.</span><span class="sxs-lookup"><span data-stu-id="7ea4e-243">Advance toohello next tutorial toolearn how toouse Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7ea4e-244">Toevoegen van een Content Delivery Network (CDN) tooan Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7ea4e-244">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)
