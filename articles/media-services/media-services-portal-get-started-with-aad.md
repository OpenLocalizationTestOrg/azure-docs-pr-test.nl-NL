---
title: aaaGet gestart met Azure AD-verificatie met behulp van hello Azure-portal | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure portal tooaccess Azure Active Directory (Azure AD) verificatie tooconsume hello Azure Media Services-API.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a>Aan de slag met Azure AD-verificatie met behulp van hello Azure-portal

Meer informatie over hoe toouse hello Azure portal tooaccess Azure Active Directory (Azure AD) verificatie tooaccess hello Azure Media Services-API.

## <a name="prerequisites"></a>Vereisten

- Een Azure-account. Als u geen account hebt, beginnen met een [gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Een Media Services-account. Zie voor meer informatie [een Azure Media Services-account maken met behulp van Azure-portal Hallo](media-services-portal-create-account.md).
- Zorg ervoor dat u bekijkt hello [toegang tot Azure Media Services-API met Azure AD authentication overzicht](media-services-use-aad-auth-to-access-ams-api.md). 

Wanneer u Azure AD-verificatie met Azure Media Services gebruikt, hebt u twee opties voor verificatie:

- **Gebruikersverificatie**. Verifiëren van een persoon met Hallo app toointeract met Media Services-resources. interactieve toepassing Hello moet eerst Hallo gebruiker gevraagd om referenties. Een voorbeeld is van een management console-app gebruikt door gemachtigde gebruikers toomonitor codering taken of live te streamen. 
- **Verificatie van de service-principal**. Een service verifiëren. Toepassingen die gebruikmaken van deze verificatiemethode vaak zijn apps die daemon-services, middelste laag services of geplande taken uitvoeren: web-apps, apps van de functie, logische apps, API's of een microservice.

> [!IMPORTANT]
> Media Services ondersteunt momenteel hello Azure Access Control-servicemodel voor verificatie. Access Control-autorisatie wordt echter op 1 juni 2018 afgeschaft. U wordt aangeraden toohello Azure AD authentication model zo snel mogelijk te migreren.

## <a name="select-hello-authentication-method"></a>Selecteer de verificatiemethode Hallo

1. In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Media Services-account.
2. Selecteren hoe tooconnect toohello Media Services-API.

    ![Selecteer op de pagina methode verbinding](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a>Gebruikersverificatie

tooconnect toohello Media Services-API met behulp van de optie voor verificatie van gebruiker hello, Hallo client-app moet toorequest een Azure AD-token heeft Hallo volgende parameters:  

* Azure AD-tenant-eindpunt
* Media Services resource-URI
* Media Services (systeemeigen) toepassing client-ID 
* Media Services (systeemeigen)-toepassing omleidings-URI 
* Resource-URI voor de REST mediaservices

U kunt Hallo waarden ophalen voor deze parameters op Hallo **Media Services-API met gebruikersverificatie** pagina. 

![Verbinding maken met verificatie op de gebruikerspagina](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

Als u verbinding toohello Media Services-API met behulp van Microsoft voor Media Services .NET SDK hello, vereist Hallo waarden zijn beschikbaar tooyou als onderdeel van Hallo SDK. Zie voor meer informatie [met Azure AD authentication tooaccess hello Azure Media Services-API met .NET](media-services-dotnet-get-started-with-aad.md).

Als u geen Hallo Media Services .NET SDK voor clients, moet u handmatig een Azure AD-tokenaanvraag maken met behulp van Hallo-parameters die eerder is besproken. Zie voor meer informatie [hoe toouse hello Azure AD Authentication Library tooget hello Azure AD-token](../active-directory/develop/active-directory-authentication-libraries.md).

## <a name="service-principal-authentication"></a>Verificatie van service-principal

tooconnect toohello Media Services-API met behulp van service-principal optie Hallo, uw app middelste laag (web-API of webtoepassing) toorequest moet een Azure AD-token heeft Hallo volgende parameters:  

* Azure AD-tenant-eindpunt
* Media Services resource-URI 
* Resource-URI voor de REST mediaservices
* Waarden van de toepassing Azure AD: Hallo **client-ID** en **clientgeheim**

U kunt Hallo waarden ophalen voor deze parameters op Hallo **tooMedia Services API verbinden met service-principal** pagina. Gebruik deze pagina toocreate een nieuwe Azure AD-toepassing of tooselect een bestaande. Nadat u hello Azure AD-app hebt geselecteerd, kunt u Haal Hallo client-ID (toepassings-ID) en Hallo client geheim (sleutel) waarden genereren. 

![Verbinding maken met de pagina van de service-principal](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

Wanneer Hallo **Service-Principal** blade wordt geopend, Hallo eerste Azure AD-toepassing die voldoet aan de volgende criteria Hallo is ingeschakeld:

- Het is een geregistreerde Azure AD-toepassing.
- Het heeft Inzender of Owner Role-Based Access Control-machtigingen op Hallo-account.

Nadat u maakt of een Azure AD-app selecteert, kunt u maken en een clientgeheim (sleutel) kopiëren en Hallo van client-ID (toepassings-ID). Hallo client geheim en client-ID zijn vereiste tooget Hallo toegangstoken in dit scenario.

Als u geen machtigingen toocreate Azure AD-apps in uw domein, hello Azure AD app besturingselementen van het Hallo-blade worden niet weergegeven en een waarschuwing wordt weergegeven.

Als u verbinding toohello Media Services-API met behulp van Media Services .NET SDK hello, Zie [met Azure AD authentication tooaccess hello Azure Media Services-API met .NET](media-services-dotnet-get-started-with-aad.md).

Als u Media Services .NET SDK voor clients in Hallo niet gebruikt, moet u handmatig een tokenaanvraag van Azure AD met Hallo-parameters die eerder is besproken. Zie voor meer informatie [hoe toouse hello Azure AD Authentication Library tooget hello Azure AD-token](../active-directory/develop/active-directory-authentication-libraries.md).

### <a name="get-hello-client-id-and-client-secret"></a>Hallo-client-ID en client geheim ophalen

Nadat u een bestaande Azure AD-app of selecteer Hallo optie toocreate een nieuwe selecteert, wordt Hallo knoppen volgende weergegeven:

![Knop machtigingen en beheren toepassing knop beheren](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

tooopen hello blade van Azure AD-toepassing, klikt u op **beheren toepassing**. Op Hallo **beheren toepassing** blade, krijgt u Hallo-app client-ID (toepassings-ID). een clientgeheim (sleutel), selecteer toogenerate **sleutels**.

![Optie voor toepassing blade sleutels beheren](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a>Machtigingen en de toepassing hello beheren

Nadat u Azure AD-toepassing hello selecteert, kunt u de toepassing hello en -machtigingen kunt beheren. tooset van uw Azure AD-toepassing tooaccess andere toepassingen, klikt u op **machtigingen beheren**. Voor beheertaken, zoals het wijzigen van sleutels en antwoord-URL's of tooedit Hallo application manifest, klikt u op **beheren toepassing**.

### <a name="edit-hello-apps-settings-or-manifest"></a>Hallo-app-instellingen bewerken of manifest

tooedit hello app-instellingen of manifest, klikt u op **beheren toepassing**.

![Toepassingspagina beheren](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a>Volgende stappen

Aan de slag met [tooyour account uploaden van bestanden](media-services-portal-upload-files.md).
