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
# <a name="how-toouse-service-management-from-python"></a>Hoe toouse servicebeheer met Python
Deze handleiding wordt getoond hoe tooprogrammatically algemene service-beheertaken uitvoeren met Python. Hallo **ServiceManagementService** klasse in Hallo [Azure SDK voor Python](https://github.com/Azure/azure-sdk-for-python) ondersteuning biedt voor toegang op programmeerniveau toomuch Hallo service management-gerelateerde functionaliteit die beschikbaar is in Hallo [Klassieke azure-portal] [ management-portal] (zoals **maken, bijwerken en verwijderen van cloud-services, implementaties, data management-services en virtuele machines**). Deze functie kan nuttig zijn bij het bouwen van toepassingen die toegang op programmeerniveau tooservice beheer moeten worden gemaakt.

## <a name="WhatIs"></a>Wat is Service Management
Hallo Service Management-API biedt toegang op programmeerniveau toomuch Hallo service management functionaliteit beschikbaar via Hallo [klassieke Azure-portal][management-portal]. Hello Azure SDK voor Python kunt u toomanage uw cloudservices en storage-accounts.

toouse hello Service Management-API, moet u te[maken van een Azure-account](https://azure.microsoft.com/pricing/free-trial/).

## <a name="Concepts"></a>Concepten
Hello Azure SDK voor Python verpakt Hallo [Azure Service Management API][svc-mgmt-rest-api], namelijk een REST-API. Alle API-bewerkingen worden uitgevoerd over SSL en wederzijds geverifieerd met X.509 v3-certificatien. Hallo-beheerservice kan vanuit een service die wordt uitgevoerd in Azure of rechtstreeks via Internet Hallo vanuit elke toepassing die u kunt een HTTPS-aanvraag verzenden en ontvangen van een HTTPS-antwoord worden benaderd.

## <a name="Installation"></a>Installatie
Alle Hallo-functies die worden beschreven in dit artikel zijn beschikbaar in Hallo `azure-servicemanagement-legacy` pakket, die u kunt installeren met behulp van pip. Zie voor meer informatie over installatie (bijvoorbeeld als u nieuwe tooPython) in dit artikel: [Python installeren en hello Azure SDK](../python-how-to-install.md)

## <a name="Connect"></a>Hoe: verbinding maken met tooservice management
tooconnect toohello Management Service-eindpunt, moet u uw Azure-abonnement-ID en een geldig beheercertificaat. U kunt uw abonnements-ID via Hallo verkrijgen [klassieke Azure-portal][management-portal].

> [!NOTE]
> Het is nu mogelijk toouse certificaten die zijn gemaakt met OpenSSL wanneer u gebruikmaakt van Windows.  Hiervoor Python punt 2.7.4 of hoger. We raden aan gebruikers toouse OpenSSL in plaats van pfx, aangezien de ondersteuning voor pfx-certificaten in de toekomst Hallo waarschijnlijk worden verwijderd.
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a>Certificaten voor op Windows of Mac/Linux (OpenSSL)
U kunt [OpenSSL](http://www.openssl.org/) toocreate uw beheercertificaat.  Moet u daadwerkelijk toocreate twee certificaten, één voor Hallo-server (een `.cer` bestand) en één voor Hallo-client (een `.pem` bestand). toocreate hello `.pem` bestand, uitvoeren:

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

toocreate hello `.cer` certificaat, uitvoeren:

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

Zie voor meer informatie over Azure certificaten [certificaten voor Azure Cloud Services-overzicht](cloud-services-certs-create.md). Zie voor een volledige beschrijving van OpenSSL parameters Hallo-documentatie op [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).

Nadat u deze bestanden hebt gemaakt, moet u tooupload hello `.cer` tooAzure via Hallo 'Uploaden' actie van het tabblad van Hallo 'Instellingen' Hallo bestand [klassieke Azure-portal][management-portal], en u moet toomake notitie van opslaglocatie Hallo `.pem` bestand.

Wanneer u uw abonnements-ID hebt ontvangen, een certificaat gemaakt en geüpload Hallo `.cer` bestand tooAzure, kunt u toohello Azure eindpunt door Hallo abonnements-id en Hallo pad toohello `.pem` bestand te**ServiceManagementService**:

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

In het voorgaande voorbeeld Hallo `sms` is een **ServiceManagementService** object. Hallo **ServiceManagementService** klasse is Hallo primaire klasse die wordt gebruikt toomanage Azure-services.

### <a name="management-certificates-on-windows-makecert"></a>Certificaten beheren in Windows (MakeCert)
U kunt een zelfondertekende beheercertificaat maken op uw machine met `makecert.exe`.  Open een **Visual Studio-opdrachtprompt** als een **beheerder** en gebruik Hallo de volgende opdracht en vervangt *AzureCertificate* met Hallo certificaatnaam gewenst toouse.

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

Hallo opdracht maakt u Hallo `.cer` -bestand en installeert u deze in Hallo **persoonlijke** certificaatarchief. Zie voor meer informatie [certificaten voor Azure Cloud Services-overzicht](cloud-services-certs-create.md).

Nadat u Hallo certificaat hebt gemaakt, moet u tooupload hello `.cer` tooAzure via Hallo 'Uploaden' actie van het tabblad van Hallo 'Instellingen' Hallo bestand [klassieke Azure-portal][management-portal].

Wanneer u uw abonnements-ID hebt ontvangen, een certificaat gemaakt en geüpload Hallo `.cer` bestand tooAzure, kunt u toohello Azure eindpunt door Hallo abonnements-id en locatie van certificaat Hallo Hallo doorgeven in uw **Persoonlijke** certificaatarchief te**ServiceManagementService** (opnieuw vervangen *AzureCertificate* met de naam van uw certificaat Hallo):

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

In het voorgaande voorbeeld Hallo `sms` is een **ServiceManagementService** object. Hallo **ServiceManagementService** klasse is Hallo primaire klasse die wordt gebruikt toomanage Azure-services.

## <a name="ListAvailableLocations"></a>Hoe: lijst met beschikbare locaties
toolist hello locaties die beschikbaar zijn voor het hosten van services, gebruik Hallo **lijst\_locaties** methode:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

Wanneer u een cloudservice of storage-service maakt, moet u een geldige locatie tooprovide. Hallo **lijst\_locaties** methode retourneert altijd een bijgewerkte lijst van de momenteel beschikbare locaties Hallo. Op dit moment van schrijven zijn Hallo beschikbare locaties:

* West-Europa
* Noord-Europa
* Zuidoost-Azië
* Oost-Azië
* VS - midden
* Noord-centraal VS
* VS - zuid/centraal
* VS - west
* VS - oost
* Japan - oost
* Japan - west
* Brazilië - zuid
* Australië - oost
* Australië - zuidoost

## <a name="CreateCloudService"></a>Hoe: Maak een cloudservice
Wanneer u een toepassing maakt en uitvoeren in Azure, Hallo code en configuratie samen heten een Azure [cloudservice] [ cloud service] (ook wel een *gehoste service* in oudere versies Azure versies). Hallo **maken\_gehost\_service** methode kunt u een nieuwe gehoste service toocreate door te geven van een gehoste service-naam (dit moet uniek zijn in Azure), een label (automatisch gecodeerde toobase64), een Beschrijving en een locatie.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

U kunt alle Hallo gehoste services voor uw abonnement Hello lijst **lijst\_gehost\_services** methode:

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

Als u informatie over een bepaalde gehoste service tooget wilt, kunt u doen door Hallo gehoste service naam toohello **ophalen\_gehost\_service\_eigenschappen** methode:

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

Nadat u een cloudservice hebt gemaakt, kunt u uw code toohello service Hello implementeren **maken\_implementatie** methode.

## <a name="DeleteCloudService"></a>Hoe: verwijderen van een service in de cloud
U kunt een cloudservice verwijderen door Hallo service naam toohello **verwijderen\_gehost\_service** methode:

    sms.delete_hosted_service('myhostedservice')

Voordat u een service verwijderen kunt, moeten alle implementaties voor Hallo-service worden verwijderd. (Zie [hoe: verwijderen van een implementatie](#DeleteDeployment) voor meer informatie.)

## <a name="DeleteDeployment"></a>Hoe: verwijderen van een implementatie
een implementatie toodelete gebruiken Hallo **verwijderen\_implementatie** methode. Hallo volgende voorbeeld laat zien hoe toodelete een implementatie met de naam `v1`.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <a name="CreateStorageService"></a>Hoe: storage-service maken
Een [opslagservice](../storage/common/storage-create-storage-account.md) hebt u toegang tooAzure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [tabellen](../cosmos-db/table-storage-how-to-use-python.md), en [wachtrijen](../storage/queues/storage-python-how-to-use-queue-storage.md). toocreate storage-service, moet u een naam voor het Hallo-service (tussen 3 en 24 tekens in kleine letters en uniek zijn binnen Azure), een beschrijving, een label (omhoog too100 tekens, automatisch gecodeerde toobase64) en een locatie. Hallo volgende voorbeeld ziet u hoe toocreate een opslag-service door een locatie te geven.

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

Houd er rekening mee in het voorgaande voorbeeld Hallo die status Hallo Hallo **maken\_opslag\_account** bewerking kan worden opgehaald door het doorgeven van Hallo resultaat geretourneerd door **maken\_opslag \_account** toohello **ophalen\_bewerking\_status** methode.  

U kunt uw storage-accounts en hun eigenschappen door hello lijst **lijst\_opslag\_accounts** methode:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <a name="DeleteStorageService"></a>Procedure: een opslagservice verwijderen
U kunt een opslagservice verwijderen door Hallo opslag service naam toohello wordt doorgegeven **verwijderen\_opslag\_account** methode. Storage-service verwijdert, worden alle gegevens die zijn opgeslagen in Hallo-service (blobs, tabellen en wachtrijen).

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <a name="ListOperatingSystems"></a>Hoe: lijst van beschikbare besturingssystemen
toolist Hallo-besturingssystemen die beschikbaar zijn voor het hosten van services, gebruiken Hallo **lijst\_besturingssysteem\_systemen** methode:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

U kunt ook hello gebruiken **lijst\_besturingssysteem\_system\_families** methode, waarmee besturingssystemen Hallo door familie groepen:

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <a name="CreateVMImage"></a>Hoe: maken van een installatiekopie van besturingssysteem
een besturingssysteem toohello installatiekopie-opslagplaats voor installatiekopieën, tooadd gebruiken Hallo **toevoegen\_os\_installatiekopie** methode:

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

toolist hello installatiekopieën van besturingssystemen die beschikbaar zijn, gebruik Hallo **lijst\_os\_installatiekopieën** methode. Het bevat alle installatiekopieën van het platform en installatiekopieën van de gebruiker:

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

## <a name="DeleteVMImage"></a>Hoe: verwijderen van een installatiekopie van besturingssysteem
een gebruikersinstallatiekopie toodelete gebruiken Hallo **verwijderen\_os\_installatiekopie** methode:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <a name="CreateVM"></a>Procedure: een virtuele machine maken
toocreate een virtuele machine, moet u eerst toocreate een [cloudservice](#CreateCloudService).  Maak vervolgens de implementatie van de virtuele machine Hallo Hallo met **maken\_virtuele\_machine\_implementatie** methode:

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

## <a name="DeleteVM"></a>Procedure: een virtuele machine verwijderen
een virtuele machine toodelete, u eerst te verwijderen Hallo-implementatie met behulp van Hallo **verwijderen\_implementatie** methode:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

Hallo-cloudservice kan vervolgens worden verwijderd met behulp van Hallo **verwijderen\_gehost\_service** methode:

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a>Procedure: Een virtuele Machine van de installatiekopie van een vastgelegde virtuele Machine maken
toocapture een VM-installatiekopie, u eerst aan te roepen Hallo **vastleggen\_vm\_installatiekopie** methode:

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

Vervolgens toomake ervoor dat u hebt het Hallo-installatiekopie is vastgelegd, hello gebruiken **lijst\_vm\_installatiekopieën** api, en zorg ervoor dat uw afbeelding wordt weergegeven in Hallo resultaten:

    images = sms.list_vm_images()

toofinally hello virtuele machine met behulp van de vastgelegde installatiekopie Hallo maken, gebruikt u Hallo **maken\_virtuele\_machine\_implementatie** methode zoals voordat, maar deze keer doorgeven in Hallo vm_image_name

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

toolearn informatie over hoe een virtuele Linux-Machine, toocapture zien [hoe tooCapture virtuele Linux-Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

toolearn informatie over hoe een virtuele Windows-computer toocapture zien [hoe tooCapture virtuele Windows-Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="What's Next"></a>Volgende stappen
Nu dat u hebt geleerd Hallo basisprincipes van service management, u toegang hebt tot Hallo [voltooid API-naslagdocumentatie voor hello Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) en voert u complexe taken eenvoudig toomanage uw toepassing python.

Zie voor meer informatie, Hallo [Python Developer Center](/develop/python/).

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
