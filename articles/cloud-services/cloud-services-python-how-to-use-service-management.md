---
title: Het gebruik van de servicebeheer-API (Python) - Functieoverzicht
description: Informatie over het programmatisch algemene service-beheertaken uitvoeren met Python.
services: cloud-services
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: 61538ec0-1536-4a7e-ae89-95967fe35d73
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/30/2017
ms.author: lmazuel
ms.openlocfilehash: 13249ba9a4b317a3154776b411ce0bb1f316b3bb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-management-from-python"></a><span data-ttu-id="d4d42-103">Het gebruik van Service Management met Python</span><span class="sxs-lookup"><span data-stu-id="d4d42-103">How to use Service Management from Python</span></span>
<span data-ttu-id="d4d42-104">Deze handleiding wordt beschreven hoe u programmatisch algemene service-beheertaken uitvoeren met Python.</span><span class="sxs-lookup"><span data-stu-id="d4d42-104">This guide shows you how to programmatically perform common service management tasks from Python.</span></span> <span data-ttu-id="d4d42-105">De **ServiceManagementService** -klasse in de [Azure SDK voor Python](https://github.com/Azure/azure-sdk-for-python) ondersteunt programmatische toegang tot veel van de service management-gerelateerde functionaliteit die beschikbaar is in de [Azure klassieke portal] [ management-portal] (zoals **maken, bijwerken en verwijderen van cloud-services, implementaties, data management-services en virtuele machines**).</span><span class="sxs-lookup"><span data-stu-id="d4d42-105">The **ServiceManagementService** class in the [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access to much of the service management-related functionality that is available in the [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="d4d42-106">Deze functie kan nuttig zijn bij het bouwen van toepassingen die programmatische toegang tot het servicebeheer van de moeten worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d4d42-106">This functionality can be useful in building applications that need programmatic access to service management.</span></span>

## <span data-ttu-id="d4d42-107"><a name="WhatIs"></a>Wat is Service Management</span><span class="sxs-lookup"><span data-stu-id="d4d42-107"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="d4d42-108">De Service Management API biedt programmatisch toegang tot veel van de service management-functionaliteit beschikbaar via de [klassieke Azure-portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="d4d42-108">The Service Management API provides programmatic access to much of the service management functionality available through the [Azure classic portal][management-portal].</span></span> <span data-ttu-id="d4d42-109">De Azure SDK voor Python kunt u uw cloudservices en storage-accounts te beheren.</span><span class="sxs-lookup"><span data-stu-id="d4d42-109">The Azure SDK for Python allows you to manage your cloud services and storage accounts.</span></span>

<span data-ttu-id="d4d42-110">Voor het gebruik van de Service Management API, moet u [maken van een Azure-account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d4d42-110">To use the Service Management API, you need to [create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="d4d42-111"><a name="Concepts"></a>Concepten</span><span class="sxs-lookup"><span data-stu-id="d4d42-111"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="d4d42-112">De Azure SDK voor Python loopt de [Azure Service Management API][svc-mgmt-rest-api], namelijk een REST-API.</span><span class="sxs-lookup"><span data-stu-id="d4d42-112">The Azure SDK for Python wraps the [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="d4d42-113">Alle API-bewerkingen worden uitgevoerd over SSL en wederzijds geverifieerd met X.509 v3-certificatien.</span><span class="sxs-lookup"><span data-stu-id="d4d42-113">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="d4d42-114">De beheerservice is toegankelijk via een service die wordt uitgevoerd in Azure of rechtstreeks toegankelijk via internet, vanuit elke toepassing die een HTTPS-verzoek kan verzenden en een HTTPS-antwoord kan ontvangen.</span><span class="sxs-lookup"><span data-stu-id="d4d42-114">The management service may be accessed from within a service running in Azure, or directly over the Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="d4d42-115"><a name="Installation"></a>Installatie</span><span class="sxs-lookup"><span data-stu-id="d4d42-115"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="d4d42-116">Alle functies die worden beschreven in dit artikel zijn beschikbaar in de `azure-servicemanagement-legacy` pakket, die u kunt installeren met behulp van pip.</span><span class="sxs-lookup"><span data-stu-id="d4d42-116">All the features described in this article are available in the `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="d4d42-117">Zie voor meer informatie over installatie (bijvoorbeeld als u niet bekend bent met Python) in dit artikel: [Python installeren en de Azure SDK](../python-how-to-install.md)</span><span class="sxs-lookup"><span data-stu-id="d4d42-117">For more information about installation (for example, if you are new to Python), see this article: [Installing Python and the Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="d4d42-118"><a name="Connect"></a>Hoe: verbinding maken met servicebeheer</span><span class="sxs-lookup"><span data-stu-id="d4d42-118"><a name="Connect"> </a>How to: Connect to service management</span></span>
<span data-ttu-id="d4d42-119">Voor verbinding met het beheer van Service-eindpunt, moet u uw Azure-abonnement-ID en een geldig beheercertificaat.</span><span class="sxs-lookup"><span data-stu-id="d4d42-119">To connect to the Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="d4d42-120">Kunt u uw abonnements-ID via de [klassieke Azure-portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="d4d42-120">You can obtain your subscription ID through the [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="d4d42-121">Het is nu mogelijk gebruik van certificaten die zijn gemaakt met OpenSSL wanneer u gebruikmaakt van Windows.</span><span class="sxs-lookup"><span data-stu-id="d4d42-121">It is now possible to use certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="d4d42-122">Hiervoor Python punt 2.7.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="d4d42-122">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="d4d42-123">U wordt aangeraden gebruikers OpenSSL gebruiken in plaats van pfx, aangezien de ondersteuning voor pfx-certificaten waarschijnlijk in de toekomst verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d4d42-123">We recommend users to use OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in the future.</span></span>
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="d4d42-124">Certificaten voor op Windows of Mac/Linux (OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="d4d42-124">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="d4d42-125">U kunt [OpenSSL](http://www.openssl.org/) voor het maken van uw beheercertificaat.</span><span class="sxs-lookup"><span data-stu-id="d4d42-125">You can use [OpenSSL](http://www.openssl.org/) to create your management certificate.</span></span>  <span data-ttu-id="d4d42-126">U moet eigenlijk twee certificaten, één voor de server maken (een `.cer` bestand) en één voor de client (een `.pem` bestand).</span><span class="sxs-lookup"><span data-stu-id="d4d42-126">You actually need to create two certificates, one for the server (a `.cer` file) and one for the client (a `.pem` file).</span></span> <span data-ttu-id="d4d42-127">Maken van de `.pem` bestand, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d4d42-127">To create the `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="d4d42-128">Maken van de `.cer` certificaat, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d4d42-128">To create the `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="d4d42-129">Zie voor meer informatie over Azure certificaten [certificaten voor Azure Cloud Services-overzicht](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="d4d42-129">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="d4d42-130">Zie de documentatie op voor een volledige beschrijving van OpenSSL parameters [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span><span class="sxs-lookup"><span data-stu-id="d4d42-130">For a complete description of OpenSSL parameters, see the documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="d4d42-131">Nadat u deze bestanden hebt gemaakt, moet u voor het uploaden van de `.cer` bestand naar Azure via de actie 'Uploaden' van het tabblad 'Instellingen' van de [klassieke Azure-portal][management-portal], en u moet Noteer waar u opgeslagen de `.pem` bestand.</span><span class="sxs-lookup"><span data-stu-id="d4d42-131">After you have created these files, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal], and you need to make note of where you saved the `.pem` file.</span></span>

<span data-ttu-id="d4d42-132">Wanneer u uw abonnements-ID hebt ontvangen, een certificaat gemaakt en geüpload de `.cer` bestand Azure, u verbinding kunt maken met het eindpunt van de Azure management door het doorgeven van de abonnements-id en het pad naar de `.pem` van het bestand in  **ServiceManagementService**:</span><span class="sxs-lookup"><span data-stu-id="d4d42-132">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the path to the `.pem` file to **ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="d4d42-133">In het voorgaande voorbeeld `sms` is een **ServiceManagementService** object.</span><span class="sxs-lookup"><span data-stu-id="d4d42-133">In the preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="d4d42-134">De **ServiceManagementService** klasse is de primaire klasse gebruikt voor het beheren van Azure-services.</span><span class="sxs-lookup"><span data-stu-id="d4d42-134">The **ServiceManagementService** class is the primary class used to manage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="d4d42-135">Certificaten beheren in Windows (MakeCert)</span><span class="sxs-lookup"><span data-stu-id="d4d42-135">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="d4d42-136">U kunt een zelfondertekende beheercertificaat maken op uw machine met `makecert.exe`.</span><span class="sxs-lookup"><span data-stu-id="d4d42-136">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="d4d42-137">Open een **Visual Studio-opdrachtprompt** als een **beheerder** en gebruikt u de volgende opdracht, vervangen *AzureCertificate* met de naam van het certificaat dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d4d42-137">Open a **Visual Studio command prompt** as an **administrator** and use the following command, replacing *AzureCertificate* with the certificate name you would like to use.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="d4d42-138">De opdracht maakt u de `.cer` -bestand en installeert deze in de **persoonlijke** certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="d4d42-138">The command creates the `.cer` file, and installs it in the **Personal** certificate store.</span></span> <span data-ttu-id="d4d42-139">Zie voor meer informatie [certificaten voor Azure Cloud Services-overzicht](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="d4d42-139">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="d4d42-140">Nadat u het certificaat hebt gemaakt, moet u voor het uploaden van de `.cer` bestand naar Azure via de actie 'Uploaden' van het tabblad 'Instellingen' van de [klassieke Azure-portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="d4d42-140">After you have created the certificate, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="d4d42-141">Wanneer u uw abonnements-ID hebt ontvangen, een certificaat gemaakt en geüpload de `.cer` bestand Azure, u verbinding kunt maken met het eindpunt van de Azure management door het doorgeven van de abonnements-id en de locatie van het certificaat in uw **persoonlijke**  certificaatarchief **ServiceManagementService** (opnieuw vervangen *AzureCertificate* met de naam van uw certificaat):</span><span class="sxs-lookup"><span data-stu-id="d4d42-141">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the location of the certificate in your **Personal** certificate store to **ServiceManagementService** (again, replace *AzureCertificate* with the name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="d4d42-142">In het voorgaande voorbeeld `sms` is een **ServiceManagementService** object.</span><span class="sxs-lookup"><span data-stu-id="d4d42-142">In the preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="d4d42-143">De **ServiceManagementService** klasse is de primaire klasse gebruikt voor het beheren van Azure-services.</span><span class="sxs-lookup"><span data-stu-id="d4d42-143">The **ServiceManagementService** class is the primary class used to manage Azure services.</span></span>

## <span data-ttu-id="d4d42-144"><a name="ListAvailableLocations"></a>Hoe: lijst met beschikbare locaties</span><span class="sxs-lookup"><span data-stu-id="d4d42-144"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="d4d42-145">U kunt de locaties die beschikbaar zijn voor het hosten van de services gebruiken de **lijst\_locaties** methode:</span><span class="sxs-lookup"><span data-stu-id="d4d42-145">To list the locations that are available for hosting services, use the **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="d4d42-146">Wanneer u een cloudservice of storage-service maakt, moet u een geldige locatie opgeeft.</span><span class="sxs-lookup"><span data-stu-id="d4d42-146">When you create a cloud service or storage service you need to provide a valid location.</span></span> <span data-ttu-id="d4d42-147">De **lijst\_locaties** methode retourneert altijd een bijgewerkte lijst van de momenteel beschikbare locaties.</span><span class="sxs-lookup"><span data-stu-id="d4d42-147">The **list\_locations** method always returns an up-to-date list of the currently available locations.</span></span> <span data-ttu-id="d4d42-148">Op dit moment van schrijven zijn de beschikbare locaties:</span><span class="sxs-lookup"><span data-stu-id="d4d42-148">As of this writing, the available locations are:</span></span>

* <span data-ttu-id="d4d42-149">West-Europa</span><span class="sxs-lookup"><span data-stu-id="d4d42-149">West Europe</span></span>
* <span data-ttu-id="d4d42-150">Noord-Europa</span><span class="sxs-lookup"><span data-stu-id="d4d42-150">North Europe</span></span>
* <span data-ttu-id="d4d42-151">Zuidoost-Azië</span><span class="sxs-lookup"><span data-stu-id="d4d42-151">Southeast Asia</span></span>
* <span data-ttu-id="d4d42-152">Oost-Azië</span><span class="sxs-lookup"><span data-stu-id="d4d42-152">East Asia</span></span>
* <span data-ttu-id="d4d42-153">VS - midden</span><span class="sxs-lookup"><span data-stu-id="d4d42-153">Central US</span></span>
* <span data-ttu-id="d4d42-154">Noord-centraal VS</span><span class="sxs-lookup"><span data-stu-id="d4d42-154">North Central US</span></span>
* <span data-ttu-id="d4d42-155">VS - zuid/centraal</span><span class="sxs-lookup"><span data-stu-id="d4d42-155">South Central US</span></span>
* <span data-ttu-id="d4d42-156">VS - west</span><span class="sxs-lookup"><span data-stu-id="d4d42-156">West US</span></span>
* <span data-ttu-id="d4d42-157">VS - oost</span><span class="sxs-lookup"><span data-stu-id="d4d42-157">East US</span></span>
* <span data-ttu-id="d4d42-158">Japan - oost</span><span class="sxs-lookup"><span data-stu-id="d4d42-158">Japan East</span></span>
* <span data-ttu-id="d4d42-159">Japan - west</span><span class="sxs-lookup"><span data-stu-id="d4d42-159">Japan West</span></span>
* <span data-ttu-id="d4d42-160">Brazilië - zuid</span><span class="sxs-lookup"><span data-stu-id="d4d42-160">Brazil South</span></span>
* <span data-ttu-id="d4d42-161">Australië - oost</span><span class="sxs-lookup"><span data-stu-id="d4d42-161">Australia East</span></span>
* <span data-ttu-id="d4d42-162">Australië - zuidoost</span><span class="sxs-lookup"><span data-stu-id="d4d42-162">Australia Southeast</span></span>

## <span data-ttu-id="d4d42-163"><a name="CreateCloudService"></a>Hoe: Maak een cloudservice</span><span class="sxs-lookup"><span data-stu-id="d4d42-163"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="d4d42-164">Wanneer u een toepassing maakt en deze in Azure uitvoeren, de code en configuratie samen heten een Azure [cloudservice] [ cloud service] (ook wel een *gehoste service* in eerdere Azure versies).</span><span class="sxs-lookup"><span data-stu-id="d4d42-164">When you create an application and run it in Azure, the code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="d4d42-165">De **maken\_gehost\_service** methode kunt u een nieuwe gehoste service maken door de naam van een gehoste service (dit moet uniek zijn in Azure), een label (automatisch naar base64 gecodeerd), een beschrijving. en een locatie.</span><span class="sxs-lookup"><span data-stu-id="d4d42-165">The **create\_hosted\_service** method allows you to create a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded to base64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="d4d42-166">U kunt alle gehoste services voor uw abonnement met de lijst de **lijst\_gehost\_services** methode:</span><span class="sxs-lookup"><span data-stu-id="d4d42-166">You can list all the hosted services for your subscription with the **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="d4d42-167">Als u informatie ophalen over een bepaalde gehoste service wilt, kunt u doen door de naam van de gehoste service voor de **ophalen\_gehost\_service\_eigenschappen** methode:</span><span class="sxs-lookup"><span data-stu-id="d4d42-167">If you want to get information about a particular hosted service, you can do so by passing the hosted service name to the **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="d4d42-168">Nadat u een cloudservice hebt gemaakt, kunt u uw code implementeren naar de service met de **maken\_implementatie** methode.</span><span class="sxs-lookup"><span data-stu-id="d4d42-168">After you have created a cloud service, you can deploy your code to the service with the **create\_deployment** method.</span></span>

## <span data-ttu-id="d4d42-169"><a name="DeleteCloudService"></a>Hoe: verwijderen van een service in de cloud</span><span class="sxs-lookup"><span data-stu-id="d4d42-169"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="d4d42-170">U kunt een cloudservice verwijderen door de naam van de service naar de **verwijderen\_gehost\_service** methode:</span><span class="sxs-lookup"><span data-stu-id="d4d42-170">You can delete a cloud service by passing the service name to the **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="d4d42-171">Voordat u een service verwijderen kunt, moeten alle implementaties voor de service worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d4d42-171">Before you can delete a service, all deployments for the service must first be deleted.</span></span> <span data-ttu-id="d4d42-172">(Zie [hoe: verwijderen van een implementatie](#DeleteDeployment) voor meer informatie.)</span><span class="sxs-lookup"><span data-stu-id="d4d42-172">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="d4d42-173"><a name="DeleteDeployment"></a>Hoe: verwijderen van een implementatie</span><span class="sxs-lookup"><span data-stu-id="d4d42-173"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="d4d42-174">Voor het verwijderen van een implementatie, gebruiken de **verwijderen\_implementatie** methode.</span><span class="sxs-lookup"><span data-stu-id="d4d42-174">To delete a deployment, use the **delete\_deployment** method.</span></span> <span data-ttu-id="d4d42-175">Het volgende voorbeeld ziet u het verwijderen van een implementatie met de naam `v1`.</span><span class="sxs-lookup"><span data-stu-id="d4d42-175">The following example shows how to delete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="d4d42-176"><a name="CreateStorageService"></a>Hoe: storage-service maken</span><span class="sxs-lookup"><span data-stu-id="d4d42-176"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="d4d42-177">Een [opslagservice](../storage/common/storage-create-storage-account.md) hebt u toegang tot Azure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [tabellen](../cosmos-db/table-storage-how-to-use-python.md), en [wachtrijen](../storage/queues/storage-python-how-to-use-queue-storage.md).</span><span class="sxs-lookup"><span data-stu-id="d4d42-177">A [storage service](../storage/common/storage-create-storage-account.md) gives you access to Azure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), and [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="d4d42-178">U moet een naam voor de service (tussen 3 en 24 tekens in kleine letters en uniek zijn binnen Azure), een beschrijving, een label (maximaal 100 tekens, automatisch naar base64 gecodeerde) en een locatie voor het maken van een storage-service.</span><span class="sxs-lookup"><span data-stu-id="d4d42-178">To create a storage service, you need a name for the service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up to 100 characters, automatically encoded to base64), and a location.</span></span> <span data-ttu-id="d4d42-179">Het volgende voorbeeld laat zien hoe een opslagservice maken door een locatie te geven.</span><span class="sxs-lookup"><span data-stu-id="d4d42-179">The following example shows how to create a storage service by specifying a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mystorageaccount'
    label = 'mystorageaccount'
    location = 'West US'
    desc = 'My storage account description.'

    result = sms.create_storage_account(name, desc, label, location=location)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="d4d42-180">Opmerking in het voorgaande voorbeeld die de status van de **maken\_opslag\_account** bewerking kan worden opgehaald door het doorgeven van het resultaat geretourneerd door **maken\_opslag\_account** naar de **ophalen\_bewerking\_status** methode.</span><span class="sxs-lookup"><span data-stu-id="d4d42-180">Note in the preceding example that the status of the **create\_storage\_account** operation can be retrieved by passing the result returned by **create\_storage\_account** to the **get\_operation\_status** method.</span></span>  

<span data-ttu-id="d4d42-181">Overzicht van uw storage-accounts en hun eigenschappen met de **lijst\_opslag\_accounts** methode:</span><span class="sxs-lookup"><span data-stu-id="d4d42-181">You can list your storage accounts and their properties with the **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="d4d42-182"><a name="DeleteStorageService"></a>Procedure: een opslagservice verwijderen</span><span class="sxs-lookup"><span data-stu-id="d4d42-182"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="d4d42-183">U kunt storage-service verwijderen door de naam van de storage-service naar de **verwijderen\_opslag\_account** methode.</span><span class="sxs-lookup"><span data-stu-id="d4d42-183">You can delete a storage service by passing the storage service name to the **delete\_storage\_account** method.</span></span> <span data-ttu-id="d4d42-184">Storage-service verwijdert, worden alle gegevens die zijn opgeslagen in de service (blobs, tabellen en wachtrijen).</span><span class="sxs-lookup"><span data-stu-id="d4d42-184">Deleting a storage service deletes all data stored in the service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="d4d42-185"><a name="ListOperatingSystems"></a>Hoe: lijst van beschikbare besturingssystemen</span><span class="sxs-lookup"><span data-stu-id="d4d42-185"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="d4d42-186">U kunt de besturingssystemen die beschikbaar zijn voor het hosten van de services gebruiken de **lijst\_besturingssysteem\_systemen** methode:</span><span class="sxs-lookup"><span data-stu-id="d4d42-186">To list the operating systems that are available for hosting services, use the **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="d4d42-187">U kunt ook de **lijst\_besturingssysteem\_system\_families** methode, waarmee de besturingssystemen die door familie groepen:</span><span class="sxs-lookup"><span data-stu-id="d4d42-187">Alternatively, you can use the **list\_operating\_system\_families** method, which groups the operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="d4d42-188"><a name="CreateVMImage"></a>Hoe: maken van een installatiekopie van besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="d4d42-188"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="d4d42-189">Als een installatiekopie van besturingssysteem toevoegen aan de opslagplaats voor installatiekopieën, gebruiken de **toevoegen\_os\_installatiekopie** methode:</span><span class="sxs-lookup"><span data-stu-id="d4d42-189">To add an operating system image to the image repository, use the **add\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mycentos'
    label = 'mycentos'
    os = 'Linux' # Linux or Windows
    media_link = 'url_to_storage_blob_for_source_image_vhd'

    result = sms.add_os_image(label, media_link, name, os)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="d4d42-190">U kunt de installatiekopieën van besturingssystemen die beschikbaar zijn, gebruiken de **lijst\_os\_installatiekopieën** methode.</span><span class="sxs-lookup"><span data-stu-id="d4d42-190">To list the operating system images that are available, use the **list\_os\_images** method.</span></span> <span data-ttu-id="d4d42-191">Het bevat alle installatiekopieën van het platform en installatiekopieën van de gebruiker:</span><span class="sxs-lookup"><span data-stu-id="d4d42-191">It includes all platform images and user images:</span></span>

    result = sms.list_os_images()

    for image in result:
        print('Name: ' + image.name)
        print('Label: ' + image.label)
        print('OS: ' + image.os)
        print('Category: ' + image.category)
        print('Description: ' + image.description)
        print('Location: ' + image.location)
        print('Media link: ' + image.media_link)
        print('')

## <span data-ttu-id="d4d42-192"><a name="DeleteVMImage"></a>Hoe: verwijderen van een installatiekopie van besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="d4d42-192"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="d4d42-193">Gebruik voor het verwijderen van de gebruikersinstallatiekopie van een de **verwijderen\_os\_installatiekopie** methode:</span><span class="sxs-lookup"><span data-stu-id="d4d42-193">To delete a user image, use the **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="d4d42-194"><a name="CreateVM"></a>Procedure: een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="d4d42-194"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="d4d42-195">Voor het maken van een virtuele machine, moet u eerst maken een [cloudservice](#CreateCloudService).</span><span class="sxs-lookup"><span data-stu-id="d4d42-195">To create a virtual machine, you first need to create a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="d4d42-196">Maak vervolgens de virtuele machine implementatie met de **maken\_virtuele\_machine\_implementatie** methode:</span><span class="sxs-lookup"><span data-stu-id="d4d42-196">Then create the virtual machine deployment using the **create\_virtual\_machine\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set the location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where the VM disk
    # will be created
    media_link = 'url_to_target_storage_blob_for_vm_hd'

    # Linux VM configuration, you can use WindowsConfigurationSet
    # for a Windows VM instead
    linux_config = LinuxConfigurationSet('myhostname', 'myuser', 'mypassword', True)

    os_hd = OSVirtualHardDisk(image_name, media_link)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=os_hd,
        role_size='Small')

## <span data-ttu-id="d4d42-197"><a name="DeleteVM"></a>Procedure: een virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="d4d42-197"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="d4d42-198">Als u wilt verwijderen van een virtuele machine, u eerst verwijderen de implementatie met behulp van de **verwijderen\_implementatie** methode:</span><span class="sxs-lookup"><span data-stu-id="d4d42-198">To delete a virtual machine, you first delete the deployment using the **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="d4d42-199">De cloudservice kan vervolgens worden verwijderd met behulp van de **verwijderen\_gehost\_service** methode:</span><span class="sxs-lookup"><span data-stu-id="d4d42-199">The cloud service can then be deleted using the **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="d4d42-200">Procedure: Een virtuele Machine van de installatiekopie van een vastgelegde virtuele Machine maken</span><span class="sxs-lookup"><span data-stu-id="d4d42-200">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="d4d42-201">Voor het vastleggen van een VM-installatiekopie, belt u eerst de **vastleggen\_vm\_installatiekopie** methode:</span><span class="sxs-lookup"><span data-stu-id="d4d42-201">To capture a VM image, you first call the **capture\_vm\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace the below three parameters with actual values
    hosted_service_name = 'hs1'
    deployment_name = 'dep1'
    vm_name = 'vm1'

    image_name = vm_name + 'image'
    image = CaptureRoleAsVMImage    ('Specialized',
        image_name,
        image_name + 'label',
        image_name + 'description',
        'english',
        'mygroup')

    result = sms.capture_vm_image(
            hosted_service_name,
            deployment_name,
            vm_name,
            image
        )

<span data-ttu-id="d4d42-202">Gebruik vervolgens om er zeker van te zijn dat u de installatiekopie hebt vastgelegd, de **lijst\_vm\_installatiekopieën** api, en zorg ervoor dat uw afbeelding wordt weergegeven in de resultaten:</span><span class="sxs-lookup"><span data-stu-id="d4d42-202">Next, to make sure that you have successfully captured the image, use the **list\_vm\_images** api, and make sure your image is displayed in the results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="d4d42-203">Ten slotte de virtuele machine met de vastgelegde installatiekopie maakt, gebruikmaken van de **maken\_virtuele\_machine\_implementatie** methode zoals voordat, maar deze keer doorgegeven in de vm_image_name</span><span class="sxs-lookup"><span data-stu-id="d4d42-203">To finally create the virtual machine using the captured image, use the **create\_virtual\_machine\_deployment** method as before, but this time pass in the vm_image_name instead</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set the location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=None,
        role_size='Small',
        vm_image_name = image_name)

<span data-ttu-id="d4d42-204">Zie voor meer informatie over het vastleggen van een virtuele Linux-Machine, [het vastleggen van een virtuele Linux-Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d4d42-204">To learn more about how to capture a Linux Virtual Machine, see [How to Capture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="d4d42-205">Zie voor meer informatie over het vastleggen van een virtuele Windows-computer, [het vastleggen van een virtuele Windows-computer.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d4d42-205">To learn more about how to capture a Windows Virtual Machine, see [How to Capture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="d4d42-206"><a name="What's Next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d4d42-206"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="d4d42-207">Nu dat u de basisprincipes van beheer-service hebt geleerd, kunt u toegang tot de [voltooid API-naslagdocumentatie voor de Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) en complexe taken gemakkelijk voor het beheren van uw toepassing python uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d4d42-207">Now that you've learned the basics of service management, you can access the [Complete API reference documentation for the Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily to manage your python application.</span></span>

<span data-ttu-id="d4d42-208">Raadpleeg het [Python Developer Center](/develop/python/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d4d42-208">For more information, see the [Python Developer Center](/develop/python/).</span></span>

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect to service management]: #Connect
[How to: List available locations]: #ListAvailableLocations
[How to: Create a cloud service]: #CreateCloudService
[How to: Delete a cloud service]: #DeleteCloudService
[How to: Create a deployment]: #CreateDeployment
[How to: Update a deployment]: #UpdateDeployment
[How to: Move deployments between staging and production]: #MoveDeployments
[How to: Delete a deployment]: #DeleteDeployment
[How to: Create a storage service]: #CreateStorageService
[How to: Delete a storage service]: #DeleteStorageService
[How to: List available operating systems]: #ListOperatingSystems
[How to: Create an operating system image]: #CreateVMImage
[How to: Delete an operating system image]: #DeleteVMImage
[How to: Create a virtual machine]: #CreateVM
[How to: Delete a virtual machine]: #DeleteVM
[Next Steps]: #NextSteps
[management-portal]: https://manage.windowsazure.com/
[svc-mgmt-rest-api]: http://msdn.microsoft.com/library/windowsazure/ee460799.aspx


[cloud service]:/services/cloud-services/
