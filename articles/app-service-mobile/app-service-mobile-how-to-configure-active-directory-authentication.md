---
title: aaaHow tooconfigure Azure Active Directory-verificatie voor uw toepassing App Services
description: Meer informatie over hoe tooconfigure Azure Active Directory-verificatie voor uw App Services-toepassing.
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: 6ec6a46c-bce4-47aa-b8a3-e133baef22eb
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5b1d73f8fdf5831a266d900cd07f4e3b0917a7f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-azure-active-directory-login"></a>Hoe tooconfigure uw App Service-toepassing toouse Azure Active Directory-aanmelding
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Dit onderwerp leest u hoe tooconfigure Azure App Services toouse Azure Active Directory als verificatieprovider.

## <a name="express"></a>Azure Active Directory configureren met behulp van snelle instellingen
1. In Hallo [Azure-portal], tooyour toepassing navigeren. Klik op **instellingen**, en vervolgens **verificatie/autorisatie**.
2. Als Hallo verificatie / autorisatie-functie niet is ingeschakeld, schakelt u Hallo switch te**op**.
3. Klik op **Azure Active Directory**, en klik vervolgens op **Express** onder **beheermodus**.
4. Klik op **OK** tooregister Hallo toepassing in Azure Active Directory. Hiermee maakt u een nieuwe registratie. Als u een bestaande registratie toochoose in plaats daarvan wilt, klikt u op **Selecteer een bestaande app** en zoek vervolgens naar het Hallo-naam van de registratie van een eerder gemaakte binnen uw tenant.
   Klik op Hallo registratie tooselect het en klik op **OK**. Klik vervolgens op **OK** op de blade hello Azure Active Directory-instellingen.
   
   ![][0]
   
   Standaard-App Service biedt verificatie maar niet beperkt geautoriseerde toegang tooyour site-inhoud en API's. U moet gebruikers machtigen in uw app-code.
5. (Optioneel) toorestrict toegang tooyour site tooonly gebruikers zijn geverifieerd door Azure Active Directory instellen **tootake actie wanneer de aanvraag is niet geverifieerd** te**aanmelden met Azure Active Directory**. Dit vereist dat alle aanvragen worden geverifieerd en alle niet-geverifieerde aanvragen worden omgeleid tooAzure Active Directory voor verificatie.
6. Klik op **Opslaan**.

U bent nu klaar toouse Azure Active Directory voor verificatie in uw app.

## <a name="advanced"></a>(Alternatieve methode) handmatig configureren van Azure Active Directory met geavanceerde instellingen
U kunt ook tooprovide configuratie-instellingen handmatig. Dit is Hallo voorkeurs-oplossing als Hallo AAD-tenant gewenst toouse verschilt van het Hallo-tenant waarmee u zich bij Azure aanmelden. toocomplete hello configuratie, moet u eerst maken een registratie in Azure Active Directory en vervolgens moet u een aantal Hallo registratie details tooApp Service.

### <a name="register"></a>Uw toepassing registreren met Azure Active Directory
1. Meld u aan toohello [Azure-portal], en ga tooyour toepassing. Kopieer uw **URL**. U gebruikt deze tooconfigure uw app in Azure Active Directory.
2. Meld u aan toohello [klassieke Azure-portal] en te navigeren**Active Directory**.
   
    ![][2]
3. Selecteer uw directory en selecteer vervolgens Hallo **toepassingen** Hallo boven op tabblad. Klik op **toevoegen** op Hallo onder toocreate een nieuwe app-registratie.
4. Klik op **mijn organisatie ontwikkelt toepassing toevoegen**.
5. In Hallo Wizard toepassing toevoegen, voert u een **naam** voor uw toepassing en klik op Hallo **webtoepassing en/of Web-API** type. Klik vervolgens op toocontinue.
6. In Hallo **AANMELDINGS-URL** vak, plak de URL van de toepassing hello u eerder hebt gekopieerd. Die dezelfde URL opgeven in Hallo **App ID URI** vak. Klik vervolgens op toocontinue.
7. Nadat de toepassing hello is toegevoegd, klikt u op Hallo **configureren** tabblad. Hallo bewerken **antwoord-URL** onder **Single Sign-on** toobe Hallo-URL van uw toepassing toegevoegd aan de Hallo pad, */.auth/login/aad/callback*. Bijvoorbeeld `https://contoso.azurewebsites.net/.auth/login/aad/callback`. Zorg ervoor dat u van Hallo HTTPS-schema gebruikmaakt.
   
    ![][3]
8. Klik op **Opslaan**. Vervolgens kopiëren Hallo **Client-ID** voor Hallo-app. Configureert u uw toepassing toouse dit later.
9. Klik in de onderste opdrachtbalk Hallo **eindpunten weergeven**, en vervolgens kopiëren Hallo **Document met federatieve metagegevens** URL en downloaden van een document of tooit in een browser navigeren.
10. Binnen de hoofdmap Hallo **EntityDescriptor** element, moet er een **id van de entiteit** Hallo vorm `https://sts.windows.net/` gevolgd door een GUID-specifieke tooyour-tenant (een 'tenant-ID' genoemd). Deze waarde voor kopiëren - fungeren als uw **URL-verlener**. Configureert u uw toepassing toouse dit later.

### <a name="secrets"></a>Azure Active Directory toevoegen informatie tooyour toepassing
1. Terug in Hallo [Azure-portal], tooyour toepassing navigeren. Klik op **instellingen**, en vervolgens **verificatie/autorisatie**.
2. Als het Hallo-verificatie/autorisatie-functie niet is ingeschakeld, schakelt u Hallo switch te**op**.
3. Klik op **Azure Active Directory**, en klik vervolgens op **Geavanceerd** onder **beheermodus**. Plakken in Hallo Client-ID en URL-verlener-waarde die u eerder hebt verkregen. Klik vervolgens op **OK**.
   
   ![][1]
   
   Standaard-App Service biedt verificatie maar niet beperkt geautoriseerde toegang tooyour site-inhoud en API's. U moet gebruikers machtigen in uw app-code.
4. (Optioneel) toorestrict toegang tooyour site tooonly gebruikers zijn geverifieerd door Azure Active Directory instellen **tootake actie wanneer de aanvraag is niet geverifieerd** te**aanmelden met Azure Active Directory**. Dit vereist dat alle aanvragen worden geverifieerd en alle niet-geverifieerde aanvragen worden omgeleid tooAzure Active Directory voor verificatie.
5. Klik op **Opslaan**.

U bent nu klaar toouse Azure Active Directory voor verificatie in uw app.

## <a name="optional-configure-a-native-client-application"></a>(Optioneel) Een systeemeigen clienttoepassing configureren
Azure Active Directory kunt u ook tooregister systeemeigen clients, waardoor meer controle over de machtigingen toewijzen. U moet dit desgewenst tooperform aanmeldingen met een bibliotheek zoals Hallo **Active Directory Authentication Library**.

1. Navigeer te**Active Directory** in Hallo [klassieke Azure-portal].
2. Selecteer uw directory en selecteer vervolgens Hallo **toepassingen** Hallo boven op tabblad. Klik op **toevoegen** op Hallo onder toocreate een nieuwe app-registratie.
3. Klik op **mijn organisatie ontwikkelt toepassing toevoegen**.
4. In Hallo Wizard toepassing toevoegen, voert u een **naam** voor uw toepassing en klik op Hallo **systeemeigen clienttoepassing** type. Klik vervolgens op toocontinue.
5. In Hallo **omleidings-URI** Voer van uw site */.auth/login/done* eindpunt, met Hallo HTTPS-schema. Deze waarde moet er ongeveer te*https://contoso.azurewebsites.net/.auth/login/done*. Als een Windows-toepassing maakt, in plaats daarvan gebruiken Hallo [pakket-SID](app-service-mobile-dotnet-how-to-use-client-library.md#package-sid) zoals Hallo URI.
6. Wanneer de systeemeigen toepassing hello is toegevoegd, klikt u op Hallo **configureren** tabblad. Hallo zoeken **Client-ID** en noteer deze waarde.
7. Scroll Hallo pagina omlaag toohello **machtigingen tooother toepassingen** sectie en klik op **toepassing toevoegen**.
8. Zoek Hallo-webtoepassing die u eerder hebt geregistreerd en klik op Hallo plus pictogram. Klik vervolgens op Hallo selectievakje tooclose Hallo dialoogvenster. Als de webtoepassing Hallo niet kan worden gevonden, gaat u tooits registratie en een nieuwe antwoord-URL (bijv, Hallo HTTP-versie van de huidige URL) toevoegen, klikt u op Opslaan en Herhaal deze stap - toepassing hello weergegeven in de lijst Hallo.
9. Open op de nieuwe vermelding Hallo u zojuist hebt toegevoegd, Hallo **gedelegeerde machtigingen** vervolgkeuzelijst en selecteer **toegang (appName)**. Klik vervolgens op **Opslaan**.

U hebt nu een native client-toepassing die uw App Service-toepassing kunt openen geconfigureerd.

## <a name="related-content"></a>Verwante inhoud
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-express-settings.png
[1]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-advanced-settings.png
[2]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-navigate-aad.png
[3]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-aad-app-configure.png

<!-- URLs. -->

[Azure-portal]: https://portal.azure.com/
[klassieke Azure-portal]: https://manage.windowsazure.com/
[alternative method]:#advanced
