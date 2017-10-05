---
title: SSL configureren voor een cloudservice (klassiek) | Microsoft Docs
description: Informatie over het opgeven van een HTTPS-eindpunt voor een Webrol en het uploaden van een SSL-certificaat voor het beveiligen van uw toepassing.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 4cbb7f38-7994-454d-b4f0-7259b558c766
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: edb9aaf6dae11c9b8a171b22bc8a17003f80d86b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="6240e-103">SSL configureren voor een toepassing in Azure</span><span class="sxs-lookup"><span data-stu-id="6240e-103">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6240e-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6240e-104">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="6240e-105">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6240e-105">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="6240e-106">SSL-versleuteling (Secure Socket Layer) is de meest gebruikte methode voor het beveiligen van gegevens die via internet worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="6240e-106">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="6240e-107">In deze algemene taak wordt beschreven hoe u een HTTPS-eindpunt kunt opgeven voor een webrol en hoe u een SSL-certificaat kunt uploaden om uw toepassing te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="6240e-107">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="6240e-108">De procedures in deze taak gelden voor Azure Cloud Services; Zie voor App-Services, [dit](../app-service-web/web-sites-configure-ssl-certificate.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="6240e-108">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span></span>
> 
> 

<span data-ttu-id="6240e-109">Deze taak maakt gebruik van een productie-implementatie.</span><span class="sxs-lookup"><span data-stu-id="6240e-109">This task uses a production deployment.</span></span> <span data-ttu-id="6240e-110">Informatie over het gebruik van een gefaseerde installatie-implementatie is verstrekt aan het einde van dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="6240e-110">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="6240e-111">Lees [dit](cloud-services-how-to-create-deploy.md) eerst artikel als u nog geen een cloudservice hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6240e-111">Read [this](cloud-services-how-to-create-deploy.md) article first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="6240e-112">Stap 1: Haal een SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="6240e-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="6240e-113">SSL configureren voor een toepassing, moet u eerst ophalen van een SSL-certificaat dat is ondertekend door een certificeringsinstantie (CA), een vertrouwde derde die certificaten voor dit doel verleent.</span><span class="sxs-lookup"><span data-stu-id="6240e-113">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="6240e-114">Als u nog geen een, moet u aanvragen bij een bedrijf dat SSL-certificaten verkoopt.</span><span class="sxs-lookup"><span data-stu-id="6240e-114">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="6240e-115">Het certificaat moet voldoen aan de volgende vereisten voor SSL-certificaten in Azure:</span><span class="sxs-lookup"><span data-stu-id="6240e-115">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="6240e-116">Het certificaat moet een persoonlijke sleutel bevatten.</span><span class="sxs-lookup"><span data-stu-id="6240e-116">The certificate must contain a private key.</span></span>
* <span data-ttu-id="6240e-117">Het certificaat moet worden gemaakt voor sleuteluitwisseling, geëxporteerd naar een bestand Personal Information Exchange (.pfx).</span><span class="sxs-lookup"><span data-stu-id="6240e-117">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="6240e-118">De onderwerpnaam van het certificaat moet overeenkomen met het domein dat wordt gebruikt voor toegang tot de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="6240e-118">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="6240e-119">U kunt een SSL-certificaat kan niet verkrijgen van een certificeringsinstantie (CA) voor het domein cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="6240e-119">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="6240e-120">Moet u een aangepaste domeinnaam moeten worden gebruikt wanneer verkrijgen toegang tot uw service.</span><span class="sxs-lookup"><span data-stu-id="6240e-120">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="6240e-121">Wanneer u een certificaat bij een Certificeringsinstantie aanvraagt, moet de onderwerpnaam van het certificaat overeenkomen met de naam van het aangepaste domein gebruikt voor toegang tot uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="6240e-121">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="6240e-122">Bijvoorbeeld, als uw aangepaste domeinnaam is **contoso.com** zou u een certificaat aanvragen van uw Certificeringsinstantie voor ***. contoso.com** of **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="6240e-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="6240e-123">Het certificaat moet ten minste 2048-bits codering gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6240e-123">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="6240e-124">Voor testdoeleinden kunt u [maken](cloud-services-certs-create.md) en een zelfondertekend certificaat gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6240e-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="6240e-125">Een zelfondertekend certificaat is niet geverifieerd via een CA en het domein cloudapp.net kunt gebruiken als de website-URL.</span><span class="sxs-lookup"><span data-stu-id="6240e-125">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="6240e-126">De volgende taak gebruikt bijvoorbeeld een zelfondertekend certificaat waarin de algemene naam (CN) gebruikt in het certificaat is **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="6240e-126">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="6240e-127">Vervolgens moet u informatie over het certificaat opnemen in uw servicedefinitie en configuratiebestanden van de service.</span><span class="sxs-lookup"><span data-stu-id="6240e-127">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="6240e-128">Stap 2: De service-definitie en configuratie van bestanden wijzigen</span><span class="sxs-lookup"><span data-stu-id="6240e-128">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="6240e-129">Uw toepassing moet worden geconfigureerd voor het gebruik van het certificaat en een HTTPS-eindpunt moet worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6240e-129">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="6240e-130">Als gevolg hiervan de servicedefinitie en configuratiebestanden van de service moeten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="6240e-130">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="6240e-131">Open het servicedefinitiebestand (CSDEF) in uw ontwikkelomgeving, voegt een **certificaten** sectie binnen de **WebRole** sectie en bevatten de volgende informatie over het certificaat (en tussenliggende certificaten):</span><span class="sxs-lookup"><span data-stu-id="6240e-131">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>
   
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
   
   <span data-ttu-id="6240e-132">De **certificaten** sectie definieert de naam van onze certificaat, de locatie en de naam van het archief waar deze zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="6240e-132">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>
   
   <span data-ttu-id="6240e-133">Machtigingen (`permisionLevel` kenmerk) kan worden ingesteld op een van de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="6240e-133">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>
   
   | <span data-ttu-id="6240e-134">Waarde van machtiging</span><span class="sxs-lookup"><span data-stu-id="6240e-134">Permission Value</span></span> | <span data-ttu-id="6240e-135">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6240e-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="6240e-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="6240e-136">limitedOrElevated</span></span> |<span data-ttu-id="6240e-137">**(Standaard)**  Alle processen van de rol toegang heeft tot de persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="6240e-137">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="6240e-138">verhoogde</span><span class="sxs-lookup"><span data-stu-id="6240e-138">elevated</span></span> |<span data-ttu-id="6240e-139">Alleen processen met verhoogde bevoegdheden hebben toegang tot de persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="6240e-139">Only elevated processes can access the private key.</span></span> |
2. <span data-ttu-id="6240e-140">Voeg in het servicedefinitiebestand een **Invoereindpunt** element in de **eindpunten** sectie HTTPS inschakelen:</span><span class="sxs-lookup"><span data-stu-id="6240e-140">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>
   
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

3. <span data-ttu-id="6240e-141">Voeg in het servicedefinitiebestand een **Binding** element in de **Sites** sectie.</span><span class="sxs-lookup"><span data-stu-id="6240e-141">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="6240e-142">Deze sectie wordt een HTTPS-binding het eindpunt toewijzen aan uw site toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="6240e-142">This section adds an HTTPS binding to map the endpoint to your site:</span></span>
   
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
   
   <span data-ttu-id="6240e-143">Alle vereiste wijzigingen in het servicedefinitiebestand zijn voltooid, maar u toch wilt gegevens van het certificaat toevoegen aan het configuratiebestand van de service.</span><span class="sxs-lookup"><span data-stu-id="6240e-143">All the required changes to the service definition file have been completed, but you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="6240e-144">Voeg in uw serviceconfiguratiebestand (CSCFG) ServiceConfiguration.Cloud.cscfg, een **certificaten** sectie binnen de **rol** sectie, vervangen de vingerafdrukwaarde van voorbeeld hieronder wordt weergegeven met die van uw certificaat:</span><span class="sxs-lookup"><span data-stu-id="6240e-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within the **Role** section, replacing the sample thumbprint value shown below with that of your certificate:</span></span>
   
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

<span data-ttu-id="6240e-145">(Maakt gebruik van het vorige voorbeeld **sha1** voor de vingerafdruk van het algoritme.</span><span class="sxs-lookup"><span data-stu-id="6240e-145">(The preceding example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="6240e-146">Geef op de juiste waarde voor de algoritme van de vingerafdruk van het certificaat.)</span><span class="sxs-lookup"><span data-stu-id="6240e-146">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="6240e-147">Nu dat de servicedefinitie en de configuratiebestanden van de service is bijgewerkt, het pakket uw implementatie voor het uploaden naar Azure.</span><span class="sxs-lookup"><span data-stu-id="6240e-147">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="6240e-148">Als u **cspack**, gebruik niet de **/generateConfigurationFile** markeren, zoals die de gegevens van het certificaat dat u ingevoegd worden overschreven.</span><span class="sxs-lookup"><span data-stu-id="6240e-148">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that overwrites the certificate information you inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="6240e-149">Stap 3: Een certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="6240e-149">Step 3: Upload a certificate</span></span>
<span data-ttu-id="6240e-150">Uw implementatiepakket is bijgewerkt om het certificaat te gebruiken en een HTTPS-eindpunt is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6240e-150">Your deployment package has been updated to use the certificate, and an HTTPS endpoint has been added.</span></span> <span data-ttu-id="6240e-151">U kunt nu het pakket en een certificaat uploaden naar Azure met de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6240e-151">Now you can upload the package and certificate to Azure with the Azure classic portal.</span></span>

1. <span data-ttu-id="6240e-152">Meld u aan bij de [klassieke Azure-portal][Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="6240e-152">Log in to the [Azure classic portal][Azure classic portal].</span></span> 
2. <span data-ttu-id="6240e-153">Klik op **Cloudservices** in het navigatievenster aan de linkerkant.</span><span class="sxs-lookup"><span data-stu-id="6240e-153">Click **Cloud Services** on the left-side navigation pane.</span></span>
3. <span data-ttu-id="6240e-154">Klik op de gewenste cloudservice.</span><span class="sxs-lookup"><span data-stu-id="6240e-154">Click the desired cloud service.</span></span>
4. <span data-ttu-id="6240e-155">Klik op de **certificaten** tabblad.</span><span class="sxs-lookup"><span data-stu-id="6240e-155">Click the **Certificates** tab.</span></span>
   
    ![Klik op het tabblad certificaten](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. <span data-ttu-id="6240e-157">Klik op de knop **Uploaden**.</span><span class="sxs-lookup"><span data-stu-id="6240e-157">Click the **Upload** button.</span></span>
   
    ![Uploaden](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. <span data-ttu-id="6240e-159">Geef de **bestand**, **wachtwoord**, klikt u vervolgens op **Complete** (het vinkje).</span><span class="sxs-lookup"><span data-stu-id="6240e-159">Provide the **File**, **Password**, then click **Complete** (the checkmark).</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="6240e-160">Stap 4: Verbinding maken met het rolexemplaar met behulp van HTTPS</span><span class="sxs-lookup"><span data-stu-id="6240e-160">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="6240e-161">Nu dat uw implementatie actief in Azure is, kunt u verbinding met het gebruik van HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6240e-161">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="6240e-162">In de klassieke Azure portal, selecteert u uw implementatie en klik op de koppeling onder **Site-URL**.</span><span class="sxs-lookup"><span data-stu-id="6240e-162">In the Azure classic portal, select your deployment, then click the link under **Site URL**.</span></span>
   
   ![Site-URL bepalen][2]
2. <span data-ttu-id="6240e-164">Wijzig de koppeling om te gebruiken in uw webbrowser **https** in plaats van **http**, en ga vervolgens naar de pagina.</span><span class="sxs-lookup"><span data-stu-id="6240e-164">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6240e-165">Als u een zelfondertekend certificaat gebruikt wanneer u naar een HTTPS-eindpunt dat is gekoppeld aan het zelfondertekende certificaat bladert, ziet u mogelijk een certificaatfout in de browser.</span><span class="sxs-lookup"><span data-stu-id="6240e-165">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="6240e-166">Met behulp van een certificaat dat is ondertekend door een vertrouwde certificeringsinstantie wordt voorkomen dat u dit probleem; in de tussentijd kunt u de fout negeren.</span><span class="sxs-lookup"><span data-stu-id="6240e-166">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="6240e-167">(Er is een andere optie is het zelfondertekende certificaat toevoegen aan certificaatarchief Vertrouwde certificaat van de gebruiker.)</span><span class="sxs-lookup"><span data-stu-id="6240e-167">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   > 
   > 
   
   ![Website voor SSL-voorbeeld][3]

<span data-ttu-id="6240e-169">Als u SSL gebruiken voor een gefaseerde installatie-implementatie in plaats van een productie-implementatie wilt, moet u eerst de URL die wordt gebruikt voor de implementatie van fasering bepalen.</span><span class="sxs-lookup"><span data-stu-id="6240e-169">If you want to use SSL for a staging deployment instead of a production deployment, you first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="6240e-170">Uw cloudservice implementeren in de testomgeving zonder een certificaat of de gegevens van een certificaat.</span><span class="sxs-lookup"><span data-stu-id="6240e-170">Deploy your cloud service to the staging environment without including a certificate or any certificate information.</span></span> <span data-ttu-id="6240e-171">Zodra geïmplementeerd, kunt u de URL op basis van GUID, die wordt vermeld in de klassieke Azure portal van bepalen **Site-URL** veld.</span><span class="sxs-lookup"><span data-stu-id="6240e-171">Once deployed, you can determine the GUID-based URL, which is listed in the Azure classic portal's **Site URL** field.</span></span> <span data-ttu-id="6240e-172">Een certificaat maken met de algemene naam (CN) gelijk zijn aan de URL op basis van GUID (bijvoorbeeld **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="6240e-172">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="6240e-173">Gebruik de klassieke Azure portal naar het certificaat toevoegen aan uw voorbereide cloudservice.</span><span class="sxs-lookup"><span data-stu-id="6240e-173">Use the Azure classic portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="6240e-174">Gegevens van het certificaat vervolgens toevoegen aan uw CSDEF- en CSCFG-bestanden, opnieuw inpakken van uw toepassing en uw gefaseerde implementatie voor het gebruik van het nieuwe pakket bijwerken.</span><span class="sxs-lookup"><span data-stu-id="6240e-174">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6240e-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6240e-175">Next steps</span></span>
* <span data-ttu-id="6240e-176">[Algemene configuratie van uw cloudservice](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="6240e-176">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="6240e-177">Meer informatie over hoe [implementeren van een cloudservice](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="6240e-177">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="6240e-178">Configureer een [aangepaste domeinnaam](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="6240e-178">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="6240e-179">[Beheren van uw cloudservice](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="6240e-179">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
