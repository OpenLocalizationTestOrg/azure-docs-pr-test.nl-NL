---
title: SSL configureren voor een cloudservice | Microsoft Docs
description: Informatie over het opgeven van een HTTPS-eindpunt voor een Webrol en het uploaden van een SSL-certificaat voor het beveiligen van uw toepassing. Deze voorbeelden worden de Azure portal gebruiken.
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
ms.openlocfilehash: e5c8c3b098772c0586712305a577b24a6f0d924c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="15c84-104">SSL configureren voor een toepassing in Azure</span><span class="sxs-lookup"><span data-stu-id="15c84-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="15c84-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="15c84-105">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="15c84-106">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="15c84-106">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
>

<span data-ttu-id="15c84-107">SSL-versleuteling (Secure Socket Layer) is de meest gebruikte methode voor het beveiligen van gegevens die via internet worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="15c84-107">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="15c84-108">In deze algemene taak wordt beschreven hoe u een HTTPS-eindpunt kunt opgeven voor een webrol en hoe u een SSL-certificaat kunt uploaden om uw toepassing te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="15c84-108">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="15c84-109">De procedures in deze taak gelden voor Azure Cloud Services; Zie voor App-Services, [dit](../app-service-web/web-sites-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="15c84-109">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).</span></span>
>

<span data-ttu-id="15c84-110">Deze taak maakt gebruik van een productie-implementatie.</span><span class="sxs-lookup"><span data-stu-id="15c84-110">This task uses a production deployment.</span></span> <span data-ttu-id="15c84-111">Informatie over het gebruik van een gefaseerde installatie-implementatie is verstrekt aan het einde van dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="15c84-111">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="15c84-112">Lees [dit](cloud-services-how-to-create-deploy-portal.md) eerste als u nog geen een cloudservice hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="15c84-112">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="15c84-113">Stap 1: Haal een SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="15c84-113">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="15c84-114">SSL configureren voor een toepassing, moet u eerst ophalen van een SSL-certificaat dat is ondertekend door een certificeringsinstantie (CA), een vertrouwde derde die certificaten voor dit doel verleent.</span><span class="sxs-lookup"><span data-stu-id="15c84-114">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="15c84-115">Als u nog geen een, moet u aanvragen bij een bedrijf dat SSL-certificaten verkoopt.</span><span class="sxs-lookup"><span data-stu-id="15c84-115">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="15c84-116">Het certificaat moet voldoen aan de volgende vereisten voor SSL-certificaten in Azure:</span><span class="sxs-lookup"><span data-stu-id="15c84-116">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="15c84-117">Het certificaat moet een persoonlijke sleutel bevatten.</span><span class="sxs-lookup"><span data-stu-id="15c84-117">The certificate must contain a private key.</span></span>
* <span data-ttu-id="15c84-118">Het certificaat moet worden gemaakt voor sleuteluitwisseling, geëxporteerd naar een bestand Personal Information Exchange (.pfx).</span><span class="sxs-lookup"><span data-stu-id="15c84-118">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="15c84-119">De onderwerpnaam van het certificaat moet overeenkomen met het domein dat wordt gebruikt voor toegang tot de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="15c84-119">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="15c84-120">U kunt een SSL-certificaat kan niet verkrijgen van een certificeringsinstantie (CA) voor het domein cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="15c84-120">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="15c84-121">Moet u een aangepaste domeinnaam moeten worden gebruikt wanneer verkrijgen toegang tot uw service.</span><span class="sxs-lookup"><span data-stu-id="15c84-121">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="15c84-122">Wanneer u een certificaat bij een Certificeringsinstantie aanvraagt, moet de onderwerpnaam van het certificaat overeenkomen met de naam van het aangepaste domein gebruikt voor toegang tot uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="15c84-122">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="15c84-123">Bijvoorbeeld, als uw aangepaste domeinnaam is **contoso.com** zou u een certificaat aanvragen van uw Certificeringsinstantie voor ***. contoso.com** of **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="15c84-123">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="15c84-124">Het certificaat moet ten minste 2048-bits codering gebruiken.</span><span class="sxs-lookup"><span data-stu-id="15c84-124">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="15c84-125">Voor testdoeleinden kunt u [maken](cloud-services-certs-create.md) en een zelfondertekend certificaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="15c84-125">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="15c84-126">Een zelfondertekend certificaat is niet geverifieerd via een CA en het domein cloudapp.net kunt gebruiken als de website-URL.</span><span class="sxs-lookup"><span data-stu-id="15c84-126">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="15c84-127">De volgende taak gebruikt bijvoorbeeld een zelfondertekend certificaat waarin de algemene naam (CN) gebruikt in het certificaat is **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="15c84-127">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="15c84-128">Vervolgens moet u informatie over het certificaat opnemen in uw servicedefinitie en configuratiebestanden van de service.</span><span class="sxs-lookup"><span data-stu-id="15c84-128">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="15c84-129"><a name="modify"> </a></span><span class="sxs-lookup"><span data-stu-id="15c84-129"><a name="modify"> </a></span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="15c84-130">Stap 2: De service-definitie en configuratie van bestanden wijzigen</span><span class="sxs-lookup"><span data-stu-id="15c84-130">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="15c84-131">Uw toepassing moet worden geconfigureerd voor het gebruik van het certificaat en een HTTPS-eindpunt moet worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="15c84-131">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="15c84-132">Als gevolg hiervan de servicedefinitie en configuratiebestanden van de service moeten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="15c84-132">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="15c84-133">Open het servicedefinitiebestand (CSDEF) in uw ontwikkelomgeving, voegt een **certificaten** sectie binnen de **WebRole** sectie en bevatten de volgende informatie over het certificaat (en tussenliggende certificaten):</span><span class="sxs-lookup"><span data-stu-id="15c84-133">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by the CA root, you
            must include all the intermediate certificates
            here. You must list them here, even if they are
            not bound to any endpoints. Failing to list any of
            the intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```

   <span data-ttu-id="15c84-134">De **certificaten** sectie definieert de naam van onze certificaat, de locatie en de naam van het archief waar deze zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="15c84-134">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>

   <span data-ttu-id="15c84-135">Machtigingen (`permisionLevel` kenmerk) kan worden ingesteld op een van de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="15c84-135">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>

   | <span data-ttu-id="15c84-136">Waarde van machtiging</span><span class="sxs-lookup"><span data-stu-id="15c84-136">Permission Value</span></span> | <span data-ttu-id="15c84-137">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="15c84-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="15c84-138">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="15c84-138">limitedOrElevated</span></span> |<span data-ttu-id="15c84-139">**(Standaard)**  Alle processen van de rol toegang heeft tot de persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="15c84-139">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="15c84-140">verhoogde</span><span class="sxs-lookup"><span data-stu-id="15c84-140">elevated</span></span> |<span data-ttu-id="15c84-141">Alleen processen met verhoogde bevoegdheden hebben toegang tot de persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="15c84-141">Only elevated processes can access the private key.</span></span> |

2. <span data-ttu-id="15c84-142">Voeg in het servicedefinitiebestand een **Invoereindpunt** element in de **eindpunten** sectie HTTPS inschakelen:</span><span class="sxs-lookup"><span data-stu-id="15c84-142">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>

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

3. <span data-ttu-id="15c84-143">Voeg in het servicedefinitiebestand een **Binding** element in de **Sites** sectie.</span><span class="sxs-lookup"><span data-stu-id="15c84-143">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="15c84-144">Dit element wordt toegevoegd een HTTPS-binding het eindpunt toewijzen aan uw site:</span><span class="sxs-lookup"><span data-stu-id="15c84-144">This element adds an HTTPS binding to map the endpoint to your site:</span></span>

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

   <span data-ttu-id="15c84-145">Alle vereiste wijzigingen in het servicedefinitiebestand zijn voltooid; maar u moet nog steeds gegevens van het certificaat toevoegen aan het configuratiebestand van de service.</span><span class="sxs-lookup"><span data-stu-id="15c84-145">All the required changes to the service definition file have been completed; but, you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="15c84-146">Voeg in uw serviceconfiguratiebestand (CSCFG) ServiceConfiguration.Cloud.cscfg, een **certificaten** waarde met die van uw certificaat.</span><span class="sxs-lookup"><span data-stu-id="15c84-146">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="15c84-147">Het volgende codevoorbeeld geeft details van de **certificaten** sectie, met uitzondering van de vingerafdrukwaarde.</span><span class="sxs-lookup"><span data-stu-id="15c84-147">The following code sample provides details of the **Certificates** section, except for the thumbprint value.</span></span>

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

<span data-ttu-id="15c84-148">(In dit voorbeeld wordt **sha1** voor de vingerafdruk van het algoritme.</span><span class="sxs-lookup"><span data-stu-id="15c84-148">(This example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="15c84-149">Geef op de juiste waarde voor de algoritme van de vingerafdruk van het certificaat.)</span><span class="sxs-lookup"><span data-stu-id="15c84-149">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="15c84-150">Nu dat de servicedefinitie en de configuratiebestanden van de service is bijgewerkt, het pakket uw implementatie voor het uploaden naar Azure.</span><span class="sxs-lookup"><span data-stu-id="15c84-150">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="15c84-151">Als u **cspack**, gebruik niet de **/generateConfigurationFile** markeren, zoals die de gegevens van het certificaat dat u zojuist hebt ingevoegd wordt overschreven.</span><span class="sxs-lookup"><span data-stu-id="15c84-151">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="15c84-152">Stap 3: Een certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="15c84-152">Step 3: Upload a certificate</span></span>
<span data-ttu-id="15c84-153">Verbinding maken met de Azure-portal en...</span><span class="sxs-lookup"><span data-stu-id="15c84-153">Connect to the Azure portal and...</span></span>

1. <span data-ttu-id="15c84-154">In de **alle resources** sectie van de Portal, selecteer uw cloudservice.</span><span class="sxs-lookup"><span data-stu-id="15c84-154">In the **All resources** section of the Portal, select your cloud service.</span></span>

    ![Uw cloudservice publiceren](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="15c84-156">Klik op **certificaten**.</span><span class="sxs-lookup"><span data-stu-id="15c84-156">Click **Certificates**.</span></span>

    ![Klik op het pictogram van certificaten](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="15c84-158">Klik op **uploaden** aan de bovenkant van het gebied van certificaten.</span><span class="sxs-lookup"><span data-stu-id="15c84-158">Click **Upload** at the top of the certificates area.</span></span>

    ![Klik op de menuopdracht uploaden](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="15c84-160">Geef de **bestand**, **wachtwoord**, klikt u vervolgens op **uploaden** onderaan in het gegevensgebied vermelding.</span><span class="sxs-lookup"><span data-stu-id="15c84-160">Provide the **File**, **Password**, then click **Upload** at the bottom of the data entry area.</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="15c84-161">Stap 4: Verbinding maken met het rolexemplaar met behulp van HTTPS</span><span class="sxs-lookup"><span data-stu-id="15c84-161">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="15c84-162">Nu dat uw implementatie actief in Azure is, kunt u verbinding met het gebruik van HTTPS.</span><span class="sxs-lookup"><span data-stu-id="15c84-162">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="15c84-163">Klik op de **Site-URL** om de webbrowser te openen.</span><span class="sxs-lookup"><span data-stu-id="15c84-163">Click the **Site URL** to open up the web browser.</span></span>

   ![Klik op de Site-URL](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="15c84-165">Wijzig de koppeling om te gebruiken in uw webbrowser **https** in plaats van **http**, en ga vervolgens naar de pagina.</span><span class="sxs-lookup"><span data-stu-id="15c84-165">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="15c84-166">Als u een zelfondertekend certificaat gebruikt wanneer u naar een HTTPS-eindpunt dat is gekoppeld aan het zelfondertekende certificaat bladert, ziet u mogelijk een certificaatfout in de browser.</span><span class="sxs-lookup"><span data-stu-id="15c84-166">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="15c84-167">Met behulp van een certificaat dat is ondertekend door een vertrouwde certificeringsinstantie wordt voorkomen dat u dit probleem; in de tussentijd kunt u de fout negeren.</span><span class="sxs-lookup"><span data-stu-id="15c84-167">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="15c84-168">(Er is een andere optie is het zelfondertekende certificaat toevoegen aan certificaatarchief Vertrouwde certificaat van de gebruiker.)</span><span class="sxs-lookup"><span data-stu-id="15c84-168">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![Voorbeeld van de site](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="15c84-170">Als u SSL gebruiken voor een gefaseerde installatie-implementatie in plaats van een productie-implementatie wilt, moet u eerst bepalen van de URL die wordt gebruikt voor de implementatie van fasering.</span><span class="sxs-lookup"><span data-stu-id="15c84-170">If you want to use SSL for a staging deployment instead of a production deployment, you'll first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="15c84-171">Zodra uw cloudservice is geïmplementeerd, de URL van de testomgeving wordt bepaald door de **implementatie-ID** GUID in deze indeling:`https://deployment-id.cloudapp.net/`</span><span class="sxs-lookup"><span data-stu-id="15c84-171">Once your cloud service has been deployed, the URL to the staging environment is determined by the **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="15c84-172">Een certificaat maken met de algemene naam (CN) gelijk zijn aan de URL op basis van GUID (bijvoorbeeld **328187776e774ceda8fc57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="15c84-172">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="15c84-173">De portal gebruiken voor het certificaat toevoegen aan uw voorbereide cloudservice.</span><span class="sxs-lookup"><span data-stu-id="15c84-173">Use the portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="15c84-174">Gegevens van het certificaat vervolgens toevoegen aan uw CSDEF- en CSCFG-bestanden, opnieuw inpakken van uw toepassing en uw gefaseerde implementatie voor het gebruik van het nieuwe pakket bijwerken.</span><span class="sxs-lookup"><span data-stu-id="15c84-174">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="15c84-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="15c84-175">Next steps</span></span>
* <span data-ttu-id="15c84-176">[Algemene configuratie van uw cloudservice](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="15c84-176">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="15c84-177">Meer informatie over hoe [implementeren van een cloudservice](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="15c84-177">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="15c84-178">Configureer een [aangepaste domeinnaam](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="15c84-178">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="15c84-179">[Beheren van uw cloudservice](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="15c84-179">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
