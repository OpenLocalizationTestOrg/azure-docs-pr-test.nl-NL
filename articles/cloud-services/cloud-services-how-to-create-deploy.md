---
title: aaaHow toocreate en implementeren van een service in de cloud | Microsoft Docs
description: Meer informatie over hoe toocreate en implementeren van een cloudservice met snelle invoer Hallo-methode in Azure.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 0ea78ccc-5e7d-40f8-bdb6-478c0eb0e265
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 09f889f81ccee6e8a7657116183aa4100410214c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>Hoe tooCreate en implementeren van een Service in de Cloud
> [!div class="op_single_selector"]
> * [Azure Portal](cloud-services-how-to-create-deploy-portal.md)
> * [Klassieke Azure Portal](cloud-services-how-to-create-deploy.md)
> 
> 

Hallo klassieke Azure portal biedt twee manieren u toocreate en implementeren van een cloudservice: **snelle invoer** en **aangepast maken**.

Dit onderwerp wordt uitgelegd hoe toouse Hallo toocreate snelle invoer voor methode een nieuwe cloudservice en gebruik vervolgens **uploaden** tooupload en implementeren van een cloud service-pakket in Azure. Wanneer u deze methode gebruikt, kunt u Hallo klassieke Azure-portal beschikbaar handige koppelingen voor het voltooien van alle vereisten die u gaat. Als u klaar toodeploy uw cloud service bent wanneer u dit hebt gemaakt, kunt u zowel op Hallo doen met behulp van dezelfde tijd **aangepast maken**.

> [!NOTE]
> Als u van plan bent toopublish uw cloudservice vanuit Visual Studio Team Services (VSTS), gebruikt u **snelle invoer**, en stel VSTS publiceren vanaf **Quick Start** of Hallo-dashboard.
> 
> 

## <a name="concepts"></a>Concepten
Drie onderdelen vereist zijn in de volgorde toodeploy een toepassing als een cloud-service in Azure:

* **Servicedefinitie**  
  Hallo cloud servicedefinitiebestand (.csdef) definieert Hallo-servicemodel, waaronder het aantal rollen Hallo.
* **Configuratie van de service**  
  Hallo cloud service-configuratiebestand (.cscfg) biedt configuratie-instellingen voor het Hallo-cloudservice en de afzonderlijke rollen, met inbegrip van het aantal rolinstanties Hallo.
* **Servicepakket**  
  Hallo-service-pakket (.cspkg) bevat Hallo toepassingscode en configuraties en het servicedefinitiebestand Hallo.

U kunt meer informatie over deze en hoe een pakket toocreate [hier](cloud-services-model-and-package.md).

## <a name="prepare-your-app"></a>Voorbereiden van uw app
Voordat u een cloudservice implementeren kunt, moet u Hallo cloud service-pakket (.cspkg) van uw toepassingscode en een cloud service-configuratiebestand (.cscfg). Hello Azure SDK biedt hulpprogramma's voor het voorbereiden van deze bestanden vereiste implementatie. U kunt vanuit Hallo Hallo SDK installeren [Azure downloadt](https://azure.microsoft.com/downloads/) pagina in Hallo taal waarin u toodevelop liever uw toepassingscode.

Drie functies van de cloud zijn speciale configuraties vereist voordat u een servicepakket exporteren:

* Als u wilt dat een cloudservice die gebruikmaakt van Secure Sockets Layer (SSL) om gegevens te coderen, toodeploy [uw toepassing configureren](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) voor SSL.
* Als u wilt dat tooconfigure extern bureaublad-verbindingen toorole exemplaren [Hallo rollen configureren](cloud-services-role-enable-remote-desktop.md) voor extern bureaublad.
* Als u tooconfigure uitgebreide bewaking voor uw cloudservice wilt, schakelt u Azure Diagnostics voor Hallo-cloudservice. *Minimale bewaking* (Hallo standaard niveau bewaking) maakt gebruik van prestatiemeteritems die afkomstig zijn van Hallo hostbesturingssystemen voor rolexemplaren (virtuele machines). ' Uitgebreide bewaking * aanvullende gegevens op basis van prestatiegegevens binnen Hallo rol exemplaren tooenable dichter analyse van problemen die tijdens de verwerking van de toepassing optreden moeten worden verzameld. toofind hoe tooenable Azure Diagnostics, Zie [diagnostische gegevens inschakelen in Azure](cloud-services-dotnet-diagnostics.md).

een cloudservice met implementaties van webrollen of werkrollen toocreate, moet u [Hallo servicepakket maken](cloud-services-model-and-package.md#servicepackagecspkg).

## <a name="before-you-begin"></a>Voordat u begint
* Als u hello Azure SDK nog niet hebt geïnstalleerd, klikt u op **Azure SDK installeren** tooopen hello [pagina Azure Downloads](https://azure.microsoft.com/downloads/), en download vervolgens het Hallo-SDK voor Hallo taal waarin u liever toodevelop uw code. (U hebt een kans toodo dit later.)
* Als alle rolinstanties een certificaat vereist, maakt u Hallo certificaten. Cloudservices moeten een pfx-bestand met een persoonlijke sleutel. U kunt [uploaden Hallo certificaten tooAzure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) bij het maken en implementeren Hallo-cloudservice.
* Als u van plan toodeploy Hallo cloud service tooan affiniteitsgroep bevinden bent, maakt u Hallo affiniteitsgroep. U kunt een affiniteitsgroep toodeploy uw cloudservice en andere toohello Azure-services gebruiken dezelfde locatie in een regio. U kunt Hallo affiniteitsgroep maken in Hallo **netwerken** gebied van de klassieke Azure-portal op Hallo Hallo **Affiniteitsgroepen** pagina.

## <a name="how-to-create-a-cloud-service-using-quick-create"></a>Hoe: Maak een cloudservice met snelle invoer
1. In Hallo [klassieke Azure-portal](http://manage.windowsazure.com/), klikt u op **nieuw**>**Compute**>**Cloudservice** > **Snelle invoer**.
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_QuickCreate.png)
2. In **URL**, voer een naam subdomein toouse in Hallo openbare URL voor toegang tot uw cloudservice in productie-implementaties. Hallo URL-indeling voor productie-implementaties is: http://*myURL*. cloudapp.net.
3. In **regio of Affiniteitsgroep**, selecteer Hallo geografische regio of affiniteitsgroep toodeploy hello cloudservice. Selecteer een affiniteitsgroep als u toodeploy uw cloud service toohello dezelfde locatie als andere Azure-services binnen een regio.
4. Klik op **Cloudservice maken**.
   
    ![CloudServices_Region](./media/cloud-services-how-to-create-deploy/CloudServices_Regionlist.png)
   
    U kunt Hallo status van Hallo proces in het berichtgedeelte Hallo Hallo onder aan Hallo venster bewaken.
   
    Hallo **Cloudservices** gebied wordt geopend, met Hallo nieuwe cloudservice weergegeven. Wanneer de status Hallo tooCreated, is cloud services te maken voltooid.
   
    ![CloudServices_CloudServicesPage](./media/cloud-services-how-to-create-deploy/CloudServices_CloudServicesPage.png)

## <a name="how-to-upload-a-certificate-for-a-cloud-service"></a>Procedure: een certificaat voor een cloudservice uploaden
1. In Hallo [klassieke Azure-portal](http://manage.windowsazure.com/), klikt u op **Cloudservices**Hallo-naam van de cloudservice Hallo op en klik vervolgens op **certificaten**.
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_EmptyDashboard.png)
2. Klik op **een certificaat uploaden** of **uploaden**.
3. In **bestand**, gebruik **Bladeren** tooselect Hallo-certificaat (.pfx-bestand).
4. In **wachtwoord**, Voer Hallo persoonlijke sleutel voor Hallo-certificaat.
5. Klik op **OK** (vinkje).
   
    ![CloudServices_AddaCertificate](./media/cloud-services-how-to-create-deploy/CloudServices_AddaCertificate.png)
   
    U kunt de voortgang Hallo Hallo is geüpload in het berichtgedeelte hello, hieronder kan bekijken. Wanneer Hallo uploaden is voltooid, Hallo certificaat toohello tabel toegevoegd. In het berichtgedeelte hello, klikt u op OK tooclose Hallo-bericht.
   
    ![CloudServices_CertificateProgress](./media/cloud-services-how-to-create-deploy/CloudServices_CertificateProgress.png)

## <a name="how-to-deploy-a-cloud-service"></a>Procedure: een cloudservice implementeren
1. In Hallo [klassieke Azure-portal](http://manage.windowsazure.com/), klikt u op **Cloudservices**Hallo-naam van de cloudservice Hallo op en klik vervolgens op **Dashboard**.
2. Klik op **uploaden van een nieuwe implementatie in productie** of **uploaden**.
3. In **implementatielabel**, voer een naam voor de nieuwe implementatie Hallo - bijvoorbeeld MyCloudServicev4.
4. In **pakket**, gebruik **Bladeren** tooselect Hallo service-pakket (.cspkg)-bestand toouse.
5. In **configuratie**, gebruik **Bladeren** tooselect Hallo service toouse bestand (.cscfg) configureren.
6. Als de cloudservice hello rollen met slechts één exemplaar bevatten wordt, schakelt u Hallo **toch implementeren als een of meer rollen met één exemplaar** selectievakje tooenable Hallo implementatie tooproceed.
   
    Azure kan alleen garanderen van 99,95% access toohello cloud-service tijdens het onderhoud en service-updates als ten minste twee exemplaren van elke rol heeft. Indien nodig, kunt u aanvullende rolinstanties toevoegen op Hallo **Scale** pagina nadat u Hallo cloudservice implementeert. Zie voor meer informatie [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).
7. Klik op **OK** (ingeschakeld) toobegin Hallo cloud service-implementatie.
   
    ![CloudServices_UploadaPackage](./media/cloud-services-how-to-create-deploy/CloudServices_UploadaPackage.png)
   
    U kunt Hallo status van de implementatie in het berichtgedeelte Hallo Hallo bewaken. Klik op OK toohide Hallo-bericht.
   
    ![CloudServices_UploadProgress](./media/cloud-services-how-to-create-deploy/CloudServices_UploadProgress.png)

## <a name="verify-your-deployment-completed-successfully"></a>Controleer of de implementatie is voltooid
1. Klik op **Dashboard**.
   
    Hallo status moet worden weergegeven dat Hallo-service is **met**.
2. Onder **snelle weergave**, klikt u op Hallo site URL tooopen uw cloudservice in een webbrowser.
   
    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy/CloudServices_QuickGlance.png)


## <a name="next-steps"></a>Volgende stappen
* [Algemene configuratie van uw cloudservice](cloud-services-how-to-configure.md).
* Configureer een [aangepaste domeinnaam](cloud-services-custom-domain-name.md).
* [Beheren van uw cloudservice](cloud-services-how-to-manage.md).
* Configureer [ssl-certificaten](cloud-services-configure-ssl-certificate.md).

