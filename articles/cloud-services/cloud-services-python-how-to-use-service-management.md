---
title: aaaHow toouse Hallo servicebeheer-API (Python) - Functieoverzicht
description: Meer informatie over hoe tooprogrammatically algemene service-beheertaken uitvoeren met Python.
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
ms.openlocfilehash: b59622203470e1586484cec4033515edb39ca4d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-management-from-python"></a><span data-ttu-id="a3e5b-103">Hoe toouse servicebeheer met Python</span><span class="sxs-lookup"><span data-stu-id="a3e5b-103">How toouse Service Management from Python</span></span>
<span data-ttu-id="a3e5b-104">Deze handleiding wordt getoond hoe tooprogrammatically algemene service-beheertaken uitvoeren met Python.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-104">This guide shows you how tooprogrammatically perform common service management tasks from Python.</span></span> <span data-ttu-id="a3e5b-105">Hallo **ServiceManagementService** klasse in Hallo [Azure SDK voor Python](https://github.com/Azure/azure-sdk-for-python) ondersteuning biedt voor toegang op programmeerniveau toomuch Hallo service management-gerelateerde functionaliteit die beschikbaar is in Hallo [Klassieke azure-portal] [ management-portal] (zoals **maken, bijwerken en verwijderen van cloud-services, implementaties, data management-services en virtuele machines**).</span><span class="sxs-lookup"><span data-stu-id="a3e5b-105">hello **ServiceManagementService** class in hello [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access toomuch of hello service management-related functionality that is available in hello [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="a3e5b-106">Deze functie kan nuttig zijn bij het bouwen van toepassingen die toegang op programmeerniveau tooservice beheer moeten worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-106">This functionality can be useful in building applications that need programmatic access tooservice management.</span></span>

## <span data-ttu-id="a3e5b-107"><a name="WhatIs"></a>Wat is Service Management</span><span class="sxs-lookup"><span data-stu-id="a3e5b-107"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="a3e5b-108">Hallo Service Management-API biedt toegang op programmeerniveau toomuch Hallo service management functionaliteit beschikbaar via Hallo [klassieke Azure-portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="a3e5b-108">hello Service Management API provides programmatic access toomuch of hello service management functionality available through hello [Azure classic portal][management-portal].</span></span> <span data-ttu-id="a3e5b-109">Hello Azure SDK voor Python kunt u toomanage uw cloudservices en storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-109">hello Azure SDK for Python allows you toomanage your cloud services and storage accounts.</span></span>

<span data-ttu-id="a3e5b-110">toouse hello Service Management-API, moet u te[maken van een Azure-account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a3e5b-110">toouse hello Service Management API, you need too[create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="a3e5b-111"><a name="Concepts"></a>Concepten</span><span class="sxs-lookup"><span data-stu-id="a3e5b-111"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="a3e5b-112">Hello Azure SDK voor Python verpakt Hallo [Azure Service Management API][svc-mgmt-rest-api], namelijk een REST-API.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-112">hello Azure SDK for Python wraps hello [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="a3e5b-113">Alle API-bewerkingen worden uitgevoerd over SSL en wederzijds geverifieerd met X.509 v3-certificatien.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-113">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="a3e5b-114">Hallo-beheerservice kan vanuit een service die wordt uitgevoerd in Azure of rechtstreeks via Internet Hallo vanuit elke toepassing die u kunt een HTTPS-aanvraag verzenden en ontvangen van een HTTPS-antwoord worden benaderd.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-114">hello management service may be accessed from within a service running in Azure, or directly over hello Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="a3e5b-115"><a name="Installation"></a>Installatie</span><span class="sxs-lookup"><span data-stu-id="a3e5b-115"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="a3e5b-116">Alle Hallo-functies die worden beschreven in dit artikel zijn beschikbaar in Hallo `azure-servicemanagement-legacy` pakket, die u kunt installeren met behulp van pip.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-116">All hello features described in this article are available in hello `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="a3e5b-117">Zie voor meer informatie over installatie (bijvoorbeeld als u nieuwe tooPython) in dit artikel: [Python installeren en hello Azure SDK](../python-how-to-install.md)</span><span class="sxs-lookup"><span data-stu-id="a3e5b-117">For more information about installation (for example, if you are new tooPython), see this article: [Installing Python and hello Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="a3e5b-118"><a name="Connect"></a>Hoe: verbinding maken met tooservice management</span><span class="sxs-lookup"><span data-stu-id="a3e5b-118"><a name="Connect"> </a>How to: Connect tooservice management</span></span>
<span data-ttu-id="a3e5b-119">tooconnect toohello Management Service-eindpunt, moet u uw Azure-abonnement-ID en een geldig beheercertificaat.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-119">tooconnect toohello Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="a3e5b-120">U kunt uw abonnements-ID via Hallo verkrijgen [klassieke Azure-portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="a3e5b-120">You can obtain your subscription ID through hello [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="a3e5b-121">Het is nu mogelijk toouse certificaten die zijn gemaakt met OpenSSL wanneer u gebruikmaakt van Windows.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-121">It is now possible toouse certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="a3e5b-122">Hiervoor Python punt 2.7.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-122">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="a3e5b-123">We raden aan gebruikers toouse OpenSSL in plaats van pfx, aangezien de ondersteuning voor pfx-certificaten in de toekomst Hallo waarschijnlijk worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-123">We recommend users toouse OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in hello future.</span></span>
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="a3e5b-124">Certificaten voor op Windows of Mac/Linux (OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="a3e5b-124">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="a3e5b-125">U kunt [OpenSSL](http://www.openssl.org/) toocreate uw beheercertificaat.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-125">You can use [OpenSSL](http://www.openssl.org/) toocreate your management certificate.</span></span>  <span data-ttu-id="a3e5b-126">Moet u daadwerkelijk toocreate twee certificaten, één voor Hallo-server (een `.cer` bestand) en één voor Hallo-client (een `.pem` bestand).</span><span class="sxs-lookup"><span data-stu-id="a3e5b-126">You actually need toocreate two certificates, one for hello server (a `.cer` file) and one for hello client (a `.pem` file).</span></span> <span data-ttu-id="a3e5b-127">toocreate hello `.pem` bestand, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-127">toocreate hello `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="a3e5b-128">toocreate hello `.cer` certificaat, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-128">toocreate hello `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="a3e5b-129">Zie voor meer informatie over Azure certificaten [certificaten voor Azure Cloud Services-overzicht](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="a3e5b-129">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="a3e5b-130">Zie voor een volledige beschrijving van OpenSSL parameters Hallo-documentatie op [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span><span class="sxs-lookup"><span data-stu-id="a3e5b-130">For a complete description of OpenSSL parameters, see hello documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="a3e5b-131">Nadat u deze bestanden hebt gemaakt, moet u tooupload hello `.cer` tooAzure via Hallo 'Uploaden' actie van het tabblad van Hallo 'Instellingen' Hallo bestand [klassieke Azure-portal][management-portal], en u moet toomake notitie van opslaglocatie Hallo `.pem` bestand.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-131">After you have created these files, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal], and you need toomake note of where you saved hello `.pem` file.</span></span>

<span data-ttu-id="a3e5b-132">Wanneer u uw abonnements-ID hebt ontvangen, een certificaat gemaakt en geüpload Hallo `.cer` bestand tooAzure, kunt u toohello Azure eindpunt door Hallo abonnements-id en Hallo pad toohello `.pem` bestand te**ServiceManagementService**:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-132">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello path toohello `.pem` file too**ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="a3e5b-133">In het voorgaande voorbeeld Hallo `sms` is een **ServiceManagementService** object.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-133">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="a3e5b-134">Hallo **ServiceManagementService** klasse is Hallo primaire klasse die wordt gebruikt toomanage Azure-services.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-134">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="a3e5b-135">Certificaten beheren in Windows (MakeCert)</span><span class="sxs-lookup"><span data-stu-id="a3e5b-135">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="a3e5b-136">U kunt een zelfondertekende beheercertificaat maken op uw machine met `makecert.exe`.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-136">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="a3e5b-137">Open een **Visual Studio-opdrachtprompt** als een **beheerder** en gebruik Hallo de volgende opdracht en vervangt *AzureCertificate* met Hallo certificaatnaam gewenst toouse.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-137">Open a **Visual Studio command prompt** as an **administrator** and use hello following command, replacing *AzureCertificate* with hello certificate name you would like toouse.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="a3e5b-138">Hallo opdracht maakt u Hallo `.cer` -bestand en installeert u deze in Hallo **persoonlijke** certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-138">hello command creates hello `.cer` file, and installs it in hello **Personal** certificate store.</span></span> <span data-ttu-id="a3e5b-139">Zie voor meer informatie [certificaten voor Azure Cloud Services-overzicht](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="a3e5b-139">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="a3e5b-140">Nadat u Hallo certificaat hebt gemaakt, moet u tooupload hello `.cer` tooAzure via Hallo 'Uploaden' actie van het tabblad van Hallo 'Instellingen' Hallo bestand [klassieke Azure-portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="a3e5b-140">After you have created hello certificate, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="a3e5b-141">Wanneer u uw abonnements-ID hebt ontvangen, een certificaat gemaakt en geüpload Hallo `.cer` bestand tooAzure, kunt u toohello Azure eindpunt door Hallo abonnements-id en locatie van certificaat Hallo Hallo doorgeven in uw **Persoonlijke** certificaatarchief te**ServiceManagementService** (opnieuw vervangen *AzureCertificate* met de naam van uw certificaat Hallo):</span><span class="sxs-lookup"><span data-stu-id="a3e5b-141">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello location of hello certificate in your **Personal** certificate store too**ServiceManagementService** (again, replace *AzureCertificate* with hello name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="a3e5b-142">In het voorgaande voorbeeld Hallo `sms` is een **ServiceManagementService** object.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-142">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="a3e5b-143">Hallo **ServiceManagementService** klasse is Hallo primaire klasse die wordt gebruikt toomanage Azure-services.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-143">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

## <span data-ttu-id="a3e5b-144"><a name="ListAvailableLocations"></a>Hoe: lijst met beschikbare locaties</span><span class="sxs-lookup"><span data-stu-id="a3e5b-144"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="a3e5b-145">toolist hello locaties die beschikbaar zijn voor het hosten van services, gebruik Hallo **lijst\_locaties** methode:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-145">toolist hello locations that are available for hosting services, use hello **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="a3e5b-146">Wanneer u een cloudservice of storage-service maakt, moet u een geldige locatie tooprovide.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-146">When you create a cloud service or storage service you need tooprovide a valid location.</span></span> <span data-ttu-id="a3e5b-147">Hallo **lijst\_locaties** methode retourneert altijd een bijgewerkte lijst van de momenteel beschikbare locaties Hallo.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-147">hello **list\_locations** method always returns an up-to-date list of hello currently available locations.</span></span> <span data-ttu-id="a3e5b-148">Op dit moment van schrijven zijn Hallo beschikbare locaties:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-148">As of this writing, hello available locations are:</span></span>

* <span data-ttu-id="a3e5b-149">West-Europa</span><span class="sxs-lookup"><span data-stu-id="a3e5b-149">West Europe</span></span>
* <span data-ttu-id="a3e5b-150">Noord-Europa</span><span class="sxs-lookup"><span data-stu-id="a3e5b-150">North Europe</span></span>
* <span data-ttu-id="a3e5b-151">Zuidoost-Azië</span><span class="sxs-lookup"><span data-stu-id="a3e5b-151">Southeast Asia</span></span>
* <span data-ttu-id="a3e5b-152">Oost-Azië</span><span class="sxs-lookup"><span data-stu-id="a3e5b-152">East Asia</span></span>
* <span data-ttu-id="a3e5b-153">VS - midden</span><span class="sxs-lookup"><span data-stu-id="a3e5b-153">Central US</span></span>
* <span data-ttu-id="a3e5b-154">Noord-centraal VS</span><span class="sxs-lookup"><span data-stu-id="a3e5b-154">North Central US</span></span>
* <span data-ttu-id="a3e5b-155">VS - zuid/centraal</span><span class="sxs-lookup"><span data-stu-id="a3e5b-155">South Central US</span></span>
* <span data-ttu-id="a3e5b-156">VS - west</span><span class="sxs-lookup"><span data-stu-id="a3e5b-156">West US</span></span>
* <span data-ttu-id="a3e5b-157">VS - oost</span><span class="sxs-lookup"><span data-stu-id="a3e5b-157">East US</span></span>
* <span data-ttu-id="a3e5b-158">Japan - oost</span><span class="sxs-lookup"><span data-stu-id="a3e5b-158">Japan East</span></span>
* <span data-ttu-id="a3e5b-159">Japan - west</span><span class="sxs-lookup"><span data-stu-id="a3e5b-159">Japan West</span></span>
* <span data-ttu-id="a3e5b-160">Brazilië - zuid</span><span class="sxs-lookup"><span data-stu-id="a3e5b-160">Brazil South</span></span>
* <span data-ttu-id="a3e5b-161">Australië - oost</span><span class="sxs-lookup"><span data-stu-id="a3e5b-161">Australia East</span></span>
* <span data-ttu-id="a3e5b-162">Australië - zuidoost</span><span class="sxs-lookup"><span data-stu-id="a3e5b-162">Australia Southeast</span></span>

## <span data-ttu-id="a3e5b-163"><a name="CreateCloudService"></a>Hoe: Maak een cloudservice</span><span class="sxs-lookup"><span data-stu-id="a3e5b-163"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="a3e5b-164">Wanneer u een toepassing maakt en uitvoeren in Azure, Hallo code en configuratie samen heten een Azure [cloudservice] [ cloud service] (ook wel een *gehoste service* in oudere versies Azure versies).</span><span class="sxs-lookup"><span data-stu-id="a3e5b-164">When you create an application and run it in Azure, hello code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="a3e5b-165">Hallo **maken\_gehost\_service** methode kunt u een nieuwe gehoste service toocreate door te geven van een gehoste service-naam (dit moet uniek zijn in Azure), een label (automatisch gecodeerde toobase64), een Beschrijving en een locatie.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-165">hello **create\_hosted\_service** method allows you toocreate a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded toobase64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="a3e5b-166">U kunt alle Hallo gehoste services voor uw abonnement Hello lijst **lijst\_gehost\_services** methode:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-166">You can list all hello hosted services for your subscription with hello **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="a3e5b-167">Als u informatie over een bepaalde gehoste service tooget wilt, kunt u doen door Hallo gehoste service naam toohello **ophalen\_gehost\_service\_eigenschappen** methode:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-167">If you want tooget information about a particular hosted service, you can do so by passing hello hosted service name toohello **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="a3e5b-168">Nadat u een cloudservice hebt gemaakt, kunt u uw code toohello service Hello implementeren **maken\_implementatie** methode.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-168">After you have created a cloud service, you can deploy your code toohello service with hello **create\_deployment** method.</span></span>

## <span data-ttu-id="a3e5b-169"><a name="DeleteCloudService"></a>Hoe: verwijderen van een service in de cloud</span><span class="sxs-lookup"><span data-stu-id="a3e5b-169"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="a3e5b-170">U kunt een cloudservice verwijderen door Hallo service naam toohello **verwijderen\_gehost\_service** methode:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-170">You can delete a cloud service by passing hello service name toohello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="a3e5b-171">Voordat u een service verwijderen kunt, moeten alle implementaties voor Hallo-service worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-171">Before you can delete a service, all deployments for hello service must first be deleted.</span></span> <span data-ttu-id="a3e5b-172">(Zie [hoe: verwijderen van een implementatie](#DeleteDeployment) voor meer informatie.)</span><span class="sxs-lookup"><span data-stu-id="a3e5b-172">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="a3e5b-173"><a name="DeleteDeployment"></a>Hoe: verwijderen van een implementatie</span><span class="sxs-lookup"><span data-stu-id="a3e5b-173"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="a3e5b-174">een implementatie toodelete gebruiken Hallo **verwijderen\_implementatie** methode.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-174">toodelete a deployment, use hello **delete\_deployment** method.</span></span> <span data-ttu-id="a3e5b-175">Hallo volgende voorbeeld laat zien hoe toodelete een implementatie met de naam `v1`.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-175">hello following example shows how toodelete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="a3e5b-176"><a name="CreateStorageService"></a>Hoe: storage-service maken</span><span class="sxs-lookup"><span data-stu-id="a3e5b-176"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="a3e5b-177">Een [opslagservice](../storage/common/storage-create-storage-account.md) hebt u toegang tooAzure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [tabellen](../cosmos-db/table-storage-how-to-use-python.md), en [wachtrijen](../storage/queues/storage-python-how-to-use-queue-storage.md).</span><span class="sxs-lookup"><span data-stu-id="a3e5b-177">A [storage service](../storage/common/storage-create-storage-account.md) gives you access tooAzure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), and [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="a3e5b-178">toocreate storage-service, moet u een naam voor het Hallo-service (tussen 3 en 24 tekens in kleine letters en uniek zijn binnen Azure), een beschrijving, een label (omhoog too100 tekens, automatisch gecodeerde toobase64) en een locatie.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-178">toocreate a storage service, you need a name for hello service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up too100 characters, automatically encoded toobase64), and a location.</span></span> <span data-ttu-id="a3e5b-179">Hallo volgende voorbeeld ziet u hoe toocreate een opslag-service door een locatie te geven.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-179">hello following example shows how toocreate a storage service by specifying a location.</span></span>

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

<span data-ttu-id="a3e5b-180">Houd er rekening mee in het voorgaande voorbeeld Hallo die status Hallo Hallo **maken\_opslag\_account** bewerking kan worden opgehaald door het doorgeven van Hallo resultaat geretourneerd door **maken\_opslag \_account** toohello **ophalen\_bewerking\_status** methode.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-180">Note in hello preceding example that hello status of hello **create\_storage\_account** operation can be retrieved by passing hello result returned by **create\_storage\_account** toohello **get\_operation\_status** method.</span></span>  

<span data-ttu-id="a3e5b-181">U kunt uw storage-accounts en hun eigenschappen door hello lijst **lijst\_opslag\_accounts** methode:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-181">You can list your storage accounts and their properties with hello **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="a3e5b-182"><a name="DeleteStorageService"></a>Procedure: een opslagservice verwijderen</span><span class="sxs-lookup"><span data-stu-id="a3e5b-182"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="a3e5b-183">U kunt een opslagservice verwijderen door Hallo opslag service naam toohello wordt doorgegeven **verwijderen\_opslag\_account** methode.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-183">You can delete a storage service by passing hello storage service name toohello **delete\_storage\_account** method.</span></span> <span data-ttu-id="a3e5b-184">Storage-service verwijdert, worden alle gegevens die zijn opgeslagen in Hallo-service (blobs, tabellen en wachtrijen).</span><span class="sxs-lookup"><span data-stu-id="a3e5b-184">Deleting a storage service deletes all data stored in hello service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="a3e5b-185"><a name="ListOperatingSystems"></a>Hoe: lijst van beschikbare besturingssystemen</span><span class="sxs-lookup"><span data-stu-id="a3e5b-185"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="a3e5b-186">toolist Hallo-besturingssystemen die beschikbaar zijn voor het hosten van services, gebruiken Hallo **lijst\_besturingssysteem\_systemen** methode:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-186">toolist hello operating systems that are available for hosting services, use hello **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="a3e5b-187">U kunt ook hello gebruiken **lijst\_besturingssysteem\_system\_families** methode, waarmee besturingssystemen Hallo door familie groepen:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-187">Alternatively, you can use hello **list\_operating\_system\_families** method, which groups hello operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="a3e5b-188"><a name="CreateVMImage"></a>Hoe: maken van een installatiekopie van besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="a3e5b-188"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="a3e5b-189">een besturingssysteem toohello installatiekopie-opslagplaats voor installatiekopieën, tooadd gebruiken Hallo **toevoegen\_os\_installatiekopie** methode:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-189">tooadd an operating system image toohello image repository, use hello **add\_os\_image** method:</span></span>

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

<span data-ttu-id="a3e5b-190">toolist hello installatiekopieën van besturingssystemen die beschikbaar zijn, gebruik Hallo **lijst\_os\_installatiekopieën** methode.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-190">toolist hello operating system images that are available, use hello **list\_os\_images** method.</span></span> <span data-ttu-id="a3e5b-191">Het bevat alle installatiekopieën van het platform en installatiekopieën van de gebruiker:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-191">It includes all platform images and user images:</span></span>

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

## <span data-ttu-id="a3e5b-192"><a name="DeleteVMImage"></a>Hoe: verwijderen van een installatiekopie van besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="a3e5b-192"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="a3e5b-193">een gebruikersinstallatiekopie toodelete gebruiken Hallo **verwijderen\_os\_installatiekopie** methode:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-193">toodelete a user image, use hello **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="a3e5b-194"><a name="CreateVM"></a>Procedure: een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="a3e5b-194"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="a3e5b-195">toocreate een virtuele machine, moet u eerst toocreate een [cloudservice](#CreateCloudService).</span><span class="sxs-lookup"><span data-stu-id="a3e5b-195">toocreate a virtual machine, you first need toocreate a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="a3e5b-196">Maak vervolgens de implementatie van de virtuele machine Hallo Hallo met **maken\_virtuele\_machine\_implementatie** methode:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-196">Then create hello virtual machine deployment using hello **create\_virtual\_machine\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where hello VM disk
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

## <span data-ttu-id="a3e5b-197"><a name="DeleteVM"></a>Procedure: een virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="a3e5b-197"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="a3e5b-198">een virtuele machine toodelete, u eerst te verwijderen Hallo-implementatie met behulp van Hallo **verwijderen\_implementatie** methode:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-198">toodelete a virtual machine, you first delete hello deployment using hello **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="a3e5b-199">Hallo-cloudservice kan vervolgens worden verwijderd met behulp van Hallo **verwijderen\_gehost\_service** methode:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-199">hello cloud service can then be deleted using hello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="a3e5b-200">Procedure: Een virtuele Machine van de installatiekopie van een vastgelegde virtuele Machine maken</span><span class="sxs-lookup"><span data-stu-id="a3e5b-200">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="a3e5b-201">toocapture een VM-installatiekopie, u eerst aan te roepen Hallo **vastleggen\_vm\_installatiekopie** methode:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-201">toocapture a VM image, you first call hello **capture\_vm\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace hello below three parameters with actual values
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

<span data-ttu-id="a3e5b-202">Vervolgens toomake ervoor dat u hebt het Hallo-installatiekopie is vastgelegd, hello gebruiken **lijst\_vm\_installatiekopieën** api, en zorg ervoor dat uw afbeelding wordt weergegeven in Hallo resultaten:</span><span class="sxs-lookup"><span data-stu-id="a3e5b-202">Next, toomake sure that you have successfully captured hello image, use hello **list\_vm\_images** api, and make sure your image is displayed in hello results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="a3e5b-203">toofinally hello virtuele machine met behulp van de vastgelegde installatiekopie Hallo maken, gebruikt u Hallo **maken\_virtuele\_machine\_implementatie** methode zoals voordat, maar deze keer doorgeven in Hallo vm_image_name</span><span class="sxs-lookup"><span data-stu-id="a3e5b-203">toofinally create hello virtual machine using hello captured image, use hello **create\_virtual\_machine\_deployment** method as before, but this time pass in hello vm_image_name instead</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
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

<span data-ttu-id="a3e5b-204">toolearn informatie over hoe een virtuele Linux-Machine, toocapture zien [hoe tooCapture virtuele Linux-Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a3e5b-204">toolearn more about how toocapture a Linux Virtual Machine, see [How tooCapture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="a3e5b-205">toolearn informatie over hoe een virtuele Windows-computer toocapture zien [hoe tooCapture virtuele Windows-Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a3e5b-205">toolearn more about how toocapture a Windows Virtual Machine, see [How tooCapture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="a3e5b-206"><a name="What's Next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a3e5b-206"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="a3e5b-207">Nu dat u hebt geleerd Hallo basisprincipes van service management, u toegang hebt tot Hallo [voltooid API-naslagdocumentatie voor hello Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) en voert u complexe taken eenvoudig toomanage uw toepassing python.</span><span class="sxs-lookup"><span data-stu-id="a3e5b-207">Now that you've learned hello basics of service management, you can access hello [Complete API reference documentation for hello Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily toomanage your python application.</span></span>

<span data-ttu-id="a3e5b-208">Zie voor meer informatie, Hallo [Python Developer Center](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="a3e5b-208">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect tooservice management]: #Connect
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
