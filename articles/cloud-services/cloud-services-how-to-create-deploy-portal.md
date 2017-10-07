---
title: aaaHow toocreate en implementeren van een service in de cloud | Microsoft Docs
description: Meer informatie over hoe toocreate en implementeren van een cloudservice met hello Azure-portal.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: dc8b81a594f3514e662c49c9a46a33da8a551f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>Hoe toocreate en implementeren van een service in de cloud
> [!div class="op_single_selector"]
> * [Azure Portal](cloud-services-how-to-create-deploy-portal.md)
> * [Klassieke Azure Portal](cloud-services-how-to-create-deploy.md)
>
>

Hello Azure portal biedt twee manieren u toocreate en implementeren van een cloudservice: *snelle invoer* en *aangepast maken*.

Dit artikel wordt uitgelegd hoe toouse Hallo toocreate snelle invoer voor methode een nieuwe cloudservice en gebruik vervolgens **uploaden** tooupload en implementeren van een cloud service-pakket in Azure. Wanneer u deze methode gebruikt, kunt u hello Azure-portal beschikbaar handige koppelingen voor het voltooien van alle vereisten die u gaat. Als u klaar toodeploy uw cloud service bent wanneer u dit hebt gemaakt, kunt u zowel op Hallo doen met behulp van aangepast maken tegelijkertijd.

> [!NOTE]
> Als u van plan bent toopublish uw cloudservice vanuit Visual Studio Team Services (VSTS), snel kunt maken en vervolgens VSTS publiceren vanuit de Azure Quickstart of Hallo dashboard Hallo instellen. Zie voor meer informatie [continue levering tooAzure door met behulp van Visual Studio Team Services][TFSTutorialForCloudService], of Zie help voor Hallo **Quick Start** pagina.
>
>

## <a name="concepts"></a>Concepten
Drie onderdelen zijn vereist toodeploy een toepassing als een cloudservice in Azure:

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

* Als u wilt dat een cloudservice die gebruikmaakt van Secure Sockets Layer (SSL) om gegevens te coderen, toodeploy [uw toepassing configureren](cloud-services-configure-ssl-certificate-portal.md#modify) voor SSL.
* Als u wilt dat tooconfigure extern bureaublad-verbindingen toorole exemplaren [Hallo rollen configureren](cloud-services-role-enable-remote-desktop-new-portal.md) voor extern bureaublad.
* Als u tooconfigure uitgebreide bewaking voor uw cloudservice wilt, schakelt u Azure Diagnostics voor Hallo-cloudservice. *Minimale bewaking* (Hallo standaard niveau bewaking) maakt gebruik van prestatiemeteritems die afkomstig zijn van Hallo hostbesturingssystemen voor rolexemplaren (virtuele machines). *Uitgebreide bewaking* aanvullende gegevens op basis van prestatiegegevens binnen Hallo rol exemplaren tooenable dichter analyse van problemen die tijdens de verwerking van de toepassing optreden moeten worden verzameld. toofind hoe tooenable Azure Diagnostics, Zie [inschakelen van diagnostische gegevens in Azure](cloud-services-dotnet-diagnostics.md).

een cloudservice met implementaties van webrollen of werkrollen toocreate, moet u [Hallo servicepakket maken](cloud-services-model-and-package.md#servicepackagecspkg).

## <a name="before-you-begin"></a>Voordat u begint
* Als u hello Azure SDK nog niet hebt geïnstalleerd, klikt u op **Azure SDK installeren** tooopen hello [pagina Azure Downloads](https://azure.microsoft.com/downloads/), en download vervolgens het Hallo-SDK voor Hallo taal waarin u liever toodevelop uw code. (U hebt een kans toodo dit later.)
* Als alle rolinstanties een certificaat vereist, maakt u Hallo certificaten. Cloudservices moeten een pfx-bestand met een persoonlijke sleutel. Bij het maken en implementeren Hallo-cloudservice, kunt u Hallo certificaten tooAzure uploaden.

## <a name="create-and-deploy"></a>Maken en implementeren
1. Meld u bij toohello [Azure-portal](https://portal.azure.com/).
2. Klik op **Nieuw > berekenen**, en schuif omlaag tooand Klik **Cloudservice**.

    ![Uw cloudservice publiceren](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. In de nieuwe Hallo **Cloudservice** blade, voer een waarde voor Hallo **DNS-naam**.
4. Maak een nieuwe **resourcegroep** of een bestaande set selecteren.
5. Selecteer een **locatie**.
6. Klik op **pakket**. Hiermee opent u Hallo **uploaden van een pakket** blade. Vul de velden Hallo vereist. Als een van de rollen één exemplaar bevatten, zorg er dan **toch implementeren als een of meer rollen met één exemplaar** is geselecteerd.
7. Zorg ervoor dat **implementatie Start** is geselecteerd.
8. Klik op **OK** die hello wordt gesloten **uploaden van een pakket** blade.
9. Als u certificaten tooadd niet hebt, klikt u op **maken**.

    ![Uw cloudservice publiceren](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a>Een certificaat uploaden
Als uw implementatiepakket [toouse certificaten geconfigureerd](cloud-services-configure-ssl-certificate-portal.md#modify), kunt u nu Hallo-certificaat uploaden.

1. Selecteer **certificaten**, en op Hallo **certificaten toevoegen** blade Hallo SSL-certificaat pfx-bestand selecteren en geef vervolgens Hallo **wachtwoord** voor Hallo-certificaat
2. Klik op **Attach certificaat**, en klik vervolgens op **OK** op Hallo **certificaten toevoegen** blade.
3. Klik op **maken** op Hallo **Cloudservice** blade. Wanneer de implementatie van Hallo Hallo heeft bereikt **gereed** status, kunt u de volgende stappen toohello doorgaan.

    ![Uw cloudservice publiceren](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a>Controleer of de implementatie is voltooid
1. Klik op Hallo cloud service-exemplaar.

    Hallo status moet worden weergegeven dat Hallo-service is **met**.
2. Onder **Essentials**, klikt u op Hallo **Site-URL** tooopen uw cloud-service in een webbrowser.

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a>Volgende stappen
* [Algemene configuratie van uw cloudservice](cloud-services-how-to-configure-portal.md).
* Configureer een [aangepaste domeinnaam](cloud-services-custom-domain-name-portal.md).
* [Beheren van uw cloudservice](cloud-services-how-to-manage-portal.md).
* Configureer [ssl-certificaten](cloud-services-configure-ssl-certificate-portal.md).
