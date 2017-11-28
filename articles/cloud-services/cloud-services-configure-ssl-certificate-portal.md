---
title: aaaConfigure SSL voor een cloudservice | Microsoft Docs
description: Meer informatie over hoe toospecify een HTTPS-eindpunt voor een Webrol en hoe tooupload een SSL-certificaat toosecure uw toepassing. Deze voorbeelden hello Azure-portal gebruiken.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 371ba204-48b6-41af-ab9f-ed1d64efe704
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: b19283bb7b0e95374f2ae9c3532eb1effc7d6a9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="0a40c-104">SSL configureren voor een toepassing in Azure</span><span class="sxs-lookup"><span data-stu-id="0a40c-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0a40c-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0a40c-105">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="0a40c-106">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0a40c-106">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
>

<span data-ttu-id="0a40c-107">Secure Socket Layer (SSL)-versleuteling is Hallo meest gebruikte methode voor het beveiligen van gegevens via Hallo verzonden van internet.</span><span class="sxs-lookup"><span data-stu-id="0a40c-107">Secure Socket Layer (SSL) encryption is hello most commonly used method of securing data sent across hello internet.</span></span> <span data-ttu-id="0a40c-108">Deze algemene taak wordt beschreven hoe toospecify een HTTPS-eindpunt voor een Webrol en hoe tooupload een SSL-certificaat toosecure uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="0a40c-108">This common task discusses how toospecify an HTTPS endpoint for a web role and how tooupload an SSL certificate toosecure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="0a40c-109">Hallo procedures in deze taak gelden tooAzure Cloudservices; Zie voor App-Services, [dit](../app-service-web/web-sites-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="0a40c-109">hello procedures in this task apply tooAzure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).</span></span>
>

<span data-ttu-id="0a40c-110">Deze taak maakt gebruik van een productie-implementatie.</span><span class="sxs-lookup"><span data-stu-id="0a40c-110">This task uses a production deployment.</span></span> <span data-ttu-id="0a40c-111">Informatie over het gebruik van een gefaseerde installatie-implementatie wordt op Hallo einde van dit onderwerp aangeboden.</span><span class="sxs-lookup"><span data-stu-id="0a40c-111">Information on using a staging deployment is provided at hello end of this topic.</span></span>

<span data-ttu-id="0a40c-112">Lees [dit](cloud-services-how-to-create-deploy-portal.md) eerste als u nog geen een cloudservice hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0a40c-112">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="0a40c-113">Stap 1: Haal een SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="0a40c-113">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="0a40c-114">tooconfigure SSL voor een toepassing, moet u eerst tooget een SSL-certificaat dat is ondertekend door een certificeringsinstantie (CA), een vertrouwde derde die certificaten voor dit doel verleent.</span><span class="sxs-lookup"><span data-stu-id="0a40c-114">tooconfigure SSL for an application, you first need tooget an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="0a40c-115">Als u nog geen een, moet u tooobtain van een bedrijf dat SSL-certificaten verkoopt.</span><span class="sxs-lookup"><span data-stu-id="0a40c-115">If you do not already have one, you need tooobtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="0a40c-116">Hallo-certificaat moet voldoen aan Hallo volgens de vereisten voor SSL-certificaten in Azure:</span><span class="sxs-lookup"><span data-stu-id="0a40c-116">hello certificate must meet hello following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="0a40c-117">Hallo-certificaat moet een persoonlijke sleutel bevatten.</span><span class="sxs-lookup"><span data-stu-id="0a40c-117">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="0a40c-118">Hallo-certificaat moet worden gemaakt voor sleuteluitwisseling, exporteerbaar tooa Personal Information Exchange (.pfx)-bestand.</span><span class="sxs-lookup"><span data-stu-id="0a40c-118">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="0a40c-119">Hallo onderwerpnaam van het certificaat moet overeenkomen met Hallo domein gebruikt tooaccess Hallo-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="0a40c-119">hello certificate's subject name must match hello domain used tooaccess hello cloud service.</span></span> <span data-ttu-id="0a40c-120">U kunt een SSL-certificaat kan niet verkrijgen van een certificeringsinstantie (CA) voor Hallo cloudapp.net domein.</span><span class="sxs-lookup"><span data-stu-id="0a40c-120">You cannot obtain an SSL certificate from a certificate authority (CA) for hello cloudapp.net domain.</span></span> <span data-ttu-id="0a40c-121">U moet een aangepast domein naam toouse verkrijgen wanneer toegang krijgen tot uw service.</span><span class="sxs-lookup"><span data-stu-id="0a40c-121">You must acquire a custom domain name toouse when access your service.</span></span> <span data-ttu-id="0a40c-122">Wanneer u een certificaat bij een Certificeringsinstantie aanvraagt, de onderwerpnaam van het Hallo-certificaat moet overeenkomen met Hallo aangepast domein naam die wordt gebruikt tooaccess uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="0a40c-122">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="0a40c-123">Bijvoorbeeld, als uw aangepaste domeinnaam is **contoso.com** zou u een certificaat aanvragen van uw Certificeringsinstantie voor ***. contoso.com** of **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="0a40c-123">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="0a40c-124">Hallo-certificaat moet ten minste 2048-bits codering gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0a40c-124">hello certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="0a40c-125">Voor testdoeleinden kunt u [maken](cloud-services-certs-create.md) en een zelfondertekend certificaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0a40c-125">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="0a40c-126">Een zelfondertekend certificaat is niet geverifieerd via een Certificeringsinstantie en Hallo cloudapp.net domein kunt gebruiken als Hallo website-URL.</span><span class="sxs-lookup"><span data-stu-id="0a40c-126">A self-signed certificate is not authenticated through a CA and can use hello cloudapp.net domain as hello website URL.</span></span> <span data-ttu-id="0a40c-127">Hallo volgende taak gebruikt bijvoorbeeld een zelfondertekend certificaat in welke Hallo is de algemene naam (CN) in Hallo certificaat gebruikt **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="0a40c-127">For example, hello following task uses a self-signed certificate in which hello common name (CN) used in hello certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="0a40c-128">Vervolgens moet u informatie over Hallo certificaat opnemen in uw servicedefinitie en configuratiebestanden van de service.</span><span class="sxs-lookup"><span data-stu-id="0a40c-128">Next, you must include information about hello certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="0a40c-129"><a name="modify"> </a></span><span class="sxs-lookup"><span data-stu-id="0a40c-129"><a name="modify"> </a></span></span>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a><span data-ttu-id="0a40c-130">Stap 2: De bestanden voor het definitie- en configuratie van de Hallo wijzigen</span><span class="sxs-lookup"><span data-stu-id="0a40c-130">Step 2: Modify hello service definition and configuration files</span></span>
<span data-ttu-id="0a40c-131">Uw toepassing moet geconfigureerde toouse Hallo certificaat en een HTTPS-eindpunt moet worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="0a40c-131">Your application must be configured toouse hello certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="0a40c-132">Als gevolg hiervan moeten hello servicedefinitie en configuratiebestanden van de service toobe bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="0a40c-132">As a result, hello service definition and service configuration files need toobe updated.</span></span>

1. <span data-ttu-id="0a40c-133">Open in uw ontwikkelomgeving Hallo servicedefinitiebestand (CSDEF), Voeg een **certificaten** sectie binnen Hallo **WebRole** sectie en bevatten Hallo volgende informatie over de certificaat (en tussenliggende certificaten):</span><span class="sxs-lookup"><span data-stu-id="0a40c-133">In your development environment, open hello service definition file (CSDEF), add a **Certificates** section within hello **WebRole** section, and include hello following information about the certificate (and intermediate certificates):</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by hello CA root, you
            must include all hello intermediate certificates
            here. You must list them here, even if they are
            not bound tooany endpoints. Failing toolist any of
            hello intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```

   <span data-ttu-id="0a40c-134">Hallo **certificaten** sectie definieert Hallo-naam van onze certificaat, de locatie en de naam op Hallo van Hallo store waar deze zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="0a40c-134">hello **Certificates** section defines hello name of our certificate, its location, and hello name of hello store where it is located.</span></span>

   <span data-ttu-id="0a40c-135">Machtigingen (`permisionLevel` kenmerk) kan worden ingesteld tooone Hallo de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="0a40c-135">Permissions (`permisionLevel` attribute) can be set tooone of hello following values:</span></span>

   | <span data-ttu-id="0a40c-136">Waarde van machtiging</span><span class="sxs-lookup"><span data-stu-id="0a40c-136">Permission Value</span></span> | <span data-ttu-id="0a40c-137">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0a40c-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="0a40c-138">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="0a40c-138">limitedOrElevated</span></span> |<span data-ttu-id="0a40c-139">**(Standaard)**  Alle processen van de rol toegang tot de persoonlijke sleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="0a40c-139">**(Default)** All role processes can access hello private key.</span></span> |
   | <span data-ttu-id="0a40c-140">verhoogde</span><span class="sxs-lookup"><span data-stu-id="0a40c-140">elevated</span></span> |<span data-ttu-id="0a40c-141">Alleen processen met verhoogde bevoegdheden hebben toegang tot de persoonlijke sleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="0a40c-141">Only elevated processes can access hello private key.</span></span> |

2. <span data-ttu-id="0a40c-142">Voeg in het servicedefinitiebestand een **Invoereindpunt** element in Hallo **eindpunten** sectie tooenable HTTPS:</span><span class="sxs-lookup"><span data-stu-id="0a40c-142">In your service definition file, add an **InputEndpoint** element within hello **Endpoints** section tooenable HTTPS:</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443"
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. <span data-ttu-id="0a40c-143">Voeg in het servicedefinitiebestand een **Binding** element in Hallo **Sites** sectie.</span><span class="sxs-lookup"><span data-stu-id="0a40c-143">In your service definition file, add a **Binding** element within hello **Sites** section.</span></span> <span data-ttu-id="0a40c-144">Dit element wordt toegevoegd een HTTPS-binding toomap de tooyour eindpunt site:</span><span class="sxs-lookup"><span data-stu-id="0a40c-144">This element adds an HTTPS binding toomap the endpoint tooyour site:</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```

   <span data-ttu-id="0a40c-145">Alle Hallo vereiste wijzigingen toohello servicedefinitiebestand zijn voltooid; maar u moet nog steeds tooadd Hallo-certificaatinformatie naar Hallo serviceconfiguratiebestand.</span><span class="sxs-lookup"><span data-stu-id="0a40c-145">All hello required changes toohello service definition file have been completed; but, you still need tooadd hello certificate information to hello service configuration file.</span></span>
4. <span data-ttu-id="0a40c-146">Voeg in uw serviceconfiguratiebestand (CSCFG) ServiceConfiguration.Cloud.cscfg, een **certificaten** waarde met die van uw certificaat.</span><span class="sxs-lookup"><span data-stu-id="0a40c-146">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="0a40c-147">Hallo volgende codevoorbeeld geeft details van Hallo **certificaten** sectie, met uitzondering van de vingerafdrukwaarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="0a40c-147">hello following code sample provides details of hello **Certificates** section, except for hello thumbprint value.</span></span>

   ```xml
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff"
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc"
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

<span data-ttu-id="0a40c-148">(In dit voorbeeld wordt **sha1** voor Hallo vingerafdruk van het algoritme.</span><span class="sxs-lookup"><span data-stu-id="0a40c-148">(This example uses **sha1** for hello thumbprint algorithm.</span></span> <span data-ttu-id="0a40c-149">Hallo geschikte waarde voor de algoritme van de vingerafdruk van het certificaat opgeven.)</span><span class="sxs-lookup"><span data-stu-id="0a40c-149">Specify hello appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="0a40c-150">Nu dat Hallo-service definitie- en configuratiebestanden zijn bijgewerkt, het pakket uw implementatie voor het uploaden van tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0a40c-150">Now that hello service definition and service configuration files have been updated, package your deployment for uploading tooAzure.</span></span> <span data-ttu-id="0a40c-151">Als u **cspack**, gebruik niet de **/generateConfigurationFile** markeren, zoals die de gegevens van het certificaat dat u zojuist hebt ingevoegd wordt overschreven.</span><span class="sxs-lookup"><span data-stu-id="0a40c-151">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="0a40c-152">Stap 3: Een certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="0a40c-152">Step 3: Upload a certificate</span></span>
<span data-ttu-id="0a40c-153">Verbinding maken met toohello Azure-portal en...</span><span class="sxs-lookup"><span data-stu-id="0a40c-153">Connect toohello Azure portal and...</span></span>

1. <span data-ttu-id="0a40c-154">In Hallo **alle resources** sectie Hallo-Portal, selecteer uw cloudservice.</span><span class="sxs-lookup"><span data-stu-id="0a40c-154">In hello **All resources** section of hello Portal, select your cloud service.</span></span>

    ![Uw cloudservice publiceren](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="0a40c-156">Klik op **certificaten**.</span><span class="sxs-lookup"><span data-stu-id="0a40c-156">Click **Certificates**.</span></span>

    ![Klik op het pictogram Hallo-certificaten](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="0a40c-158">Klik op **uploaden** bovenaan Hallo Hallo certificaten gebied.</span><span class="sxs-lookup"><span data-stu-id="0a40c-158">Click **Upload** at hello top of hello certificates area.</span></span>

    ![Klik op Hallo uploaden menu-item](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="0a40c-160">Hallo bieden **bestand**, **wachtwoord**, klikt u vervolgens op **uploaden** Hallo Hallo vermelding gegevensgebied onderaan in.</span><span class="sxs-lookup"><span data-stu-id="0a40c-160">Provide hello **File**, **Password**, then click **Upload** at hello bottom of hello data entry area.</span></span>

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a><span data-ttu-id="0a40c-161">Stap 4: Toohello rolinstantie verbinding via HTTPS</span><span class="sxs-lookup"><span data-stu-id="0a40c-161">Step 4: Connect toohello role instance by using HTTPS</span></span>
<span data-ttu-id="0a40c-162">Nu dat uw implementatie actief in Azure is, kunt u tooit via HTTPS verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="0a40c-162">Now that your deployment is up and running in Azure, you can connect tooit using HTTPS.</span></span>

1. <span data-ttu-id="0a40c-163">Klik op Hallo **Site-URL** tooopen up Hallo webbrowser.</span><span class="sxs-lookup"><span data-stu-id="0a40c-163">Click hello **Site URL** tooopen up hello web browser.</span></span>

   ![Klik op Hallo Site-URL](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="0a40c-165">Wijzig in uw webbrowser Hallo koppeling toouse **https** in plaats van **http**, en Ga naar de pagina Hallo.</span><span class="sxs-lookup"><span data-stu-id="0a40c-165">In your web browser, modify hello link toouse **https** instead of **http**, and then visit hello page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0a40c-166">Als u een zelfondertekend certificaat gebruikt wanneer u HTTPS-eindpunt voor tooan die is gekoppeld aan de zelf-ondertekend certificaat Hallo bladert, ziet u mogelijk een certificaatfout in Hallo browser.</span><span class="sxs-lookup"><span data-stu-id="0a40c-166">If you are using a self-signed certificate, when you browse tooan HTTPS endpoint that's associated with hello self-signed certificate you may see a certificate error in hello browser.</span></span> <span data-ttu-id="0a40c-167">Met behulp van een certificaat dat is ondertekend door een vertrouwde certificeringsinstantie wordt voorkomen dat u dit probleem; in Hallo kunt u tussentijd Hallo fout negeren.</span><span class="sxs-lookup"><span data-stu-id="0a40c-167">Using a certificate signed by a trusted certification authority eliminates this problem; in hello meantime, you can ignore hello error.</span></span> <span data-ttu-id="0a40c-168">(Een andere optie is certificaatarchief Vertrouwde certificaat tooadd Hallo zelf-ondertekend certificaat toohello van gebruiker.)</span><span class="sxs-lookup"><span data-stu-id="0a40c-168">(Another option is tooadd hello self-signed certificate toohello user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![Voorbeeld van de site](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="0a40c-170">Als u toouse SSL voor een gefaseerde installatie-implementatie in plaats van een productie-implementatie wilt, moet u eerst toodetermine Hallo-URL die wordt gebruikt voor Hallo staging-implementatie.</span><span class="sxs-lookup"><span data-stu-id="0a40c-170">If you want toouse SSL for a staging deployment instead of a production deployment, you'll first need toodetermine hello URL used for hello staging deployment.</span></span> <span data-ttu-id="0a40c-171">Zodra uw cloudservice is geïmplementeerd, Hallo URL toohello staging-omgeving wordt bepaald door Hallo **implementatie-ID** GUID in deze indeling:`https://deployment-id.cloudapp.net/`</span><span class="sxs-lookup"><span data-stu-id="0a40c-171">Once your cloud service has been deployed, hello URL toohello staging environment is determined by hello **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="0a40c-172">Een certificaat maken met de Hallo algemene naam (CN) gelijk toohello op basis van GUID-URL (bijvoorbeeld **328187776e774ceda8fc57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="0a40c-172">Create a certificate with hello common name (CN) equal toohello GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="0a40c-173">Gebruik Hallo portal tooadd Hallo certificaat tooyour gefaseerde service in de cloud.</span><span class="sxs-lookup"><span data-stu-id="0a40c-173">Use hello portal tooadd hello certificate tooyour staged cloud service.</span></span> <span data-ttu-id="0a40c-174">Voeg Hallo informatie tooyour CSDEF- en CSCFG-certificaatbestanden, opnieuw inpakken van uw toepassing en uw gefaseerde implementatie toouse Hallo nieuw pakket bijwerken.</span><span class="sxs-lookup"><span data-stu-id="0a40c-174">Then, add hello certificate information tooyour CSDEF and CSCFG files, repackage your application, and update your staged deployment toouse hello new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="0a40c-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0a40c-175">Next steps</span></span>
* <span data-ttu-id="0a40c-176">[Algemene configuratie van uw cloudservice](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0a40c-176">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="0a40c-177">Meer informatie over hoe te[implementeren van een cloudservice](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0a40c-177">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="0a40c-178">Configureer een [aangepaste domeinnaam](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0a40c-178">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="0a40c-179">[Beheren van uw cloudservice](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0a40c-179">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
