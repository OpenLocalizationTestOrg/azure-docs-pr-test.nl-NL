---
title: Het configureren van Azure Active Directory-verificatie voor uw toepassing App Services
description: Informatie over het configureren van Azure Active Directory-verificatie voor uw App Services-toepassing.
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
ms.openlocfilehash: fe007fa8640d5641f29dc88f8f3a8ca52a1ca8ae
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-azure-active-directory-login"></a>Uw App Service-toepassing configureren voor het gebruik van Azure Active Directory-aanmelding
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Dit onderwerp leest u over het configureren van Azure App Services voor het gebruik van Azure Active Directory als verificatieprovider.

## <a name="express"></a>Azure Active Directory configureren met behulp van snelle instellingen
1. In de [Azure-portal], gaat u naar uw toepassing. Klik op **instellingen**, en vervolgens **verificatie/autorisatie**.
2. Als de verificatie / autorisatie-functie niet is ingeschakeld, schakelt u de schakeloptie voor **op**.
3. Klik op **Azure Active Directory**, en klik vervolgens op **Express** onder **beheermodus**.
4. Klik op **OK** registreren van de toepassing in Azure Active Directory. Hiermee maakt u een nieuwe registratie. Als u een bestaande registratie in plaats daarvan kiezen wilt, klikt u op **Selecteer een bestaande app** en zoek vervolgens naar de naam van de registratie van een eerder gemaakte binnen uw tenant.
   Klik op de registratie te selecteren en klik op **OK**. Klik vervolgens op **OK** op de blade voor Azure Active Directory-instellingen.
   
   ![][0]
   
   Standaard-App Service biedt verificatie maar wordt niet geautoriseerde toegang beperkt tot uw site-inhoud en API's. U moet gebruikers machtigen in uw app-code.
5. (Optioneel) Instellen om toegang te beperken tot uw site tot alleen gebruikers die zijn geverifieerd door Azure Active Directory, **te ondernemen actie wanneer de aanvraag is niet geverifieerd** naar **aanmelden met Azure Active Directory**. Dit vereist dat alle aanvragen worden geverifieerd en alle niet-geverifieerde aanvragen worden omgeleid naar Azure Active Directory voor verificatie.
6. Klik op **Opslaan**.

U bent nu klaar voor gebruik van Azure Active Directory voor verificatie in uw app.

## <a name="advanced"></a>(Alternatieve methode) handmatig configureren van Azure Active Directory met geavanceerde instellingen
U kunt er ook voor kiezen om configuratie-instellingen handmatig. Dit is de beste oplossing als de AAD-tenant die u wilt gebruiken, wijkt af van de tenant waarmee u zich bij Azure aanmelden. Voor het voltooien van de configuratie, moet u eerst een registratie in Azure Active Directory maken en vervolgens u enkele van de registratiedetails van de in App Service moet opgeven.

### <a name="register"></a>Uw toepassing registreren met Azure Active Directory
1. Meld u aan bij de [Azure-portal], en navigeer naar uw toepassing. Kopieer uw **URL**. U gebruikt dit voor het configureren van uw app in Azure Active Directory.
2. Aanmelden bij de [klassieke Azure-portal] en navigeer naar **Active Directory**.
   
    ![][2]
3. Selecteer uw directory en selecteer vervolgens de **toepassingen** boven op het tabblad. Klik op **toevoegen** onder een nieuwe app-registratie maken.
4. Klik op **mijn organisatie ontwikkelt toepassing toevoegen**.
5. Voer in de Wizard toepassing toevoegen, een **naam** voor uw toepassing en klik op de **webtoepassing en/of Web-API** type. Klik vervolgens op om door te gaan.
6. In de **AANMELDINGS-URL** vak, plak de URL van de toepassing die u eerder hebt gekopieerd. Voer dezelfde URL in de **App ID URI** vak. Klik vervolgens op om door te gaan.
7. Nadat de toepassing is toegevoegd, klikt u op de **configureren** tabblad. Bewerk de **antwoord-URL** onder **Single Sign-on** moet de URL van uw toepassing toegevoegd aan het pad */.auth/login/aad/callback*. Bijvoorbeeld `https://contoso.azurewebsites.net/.auth/login/aad/callback`. Zorg ervoor dat u van het HTTPS-schema gebruikmaakt.
   
    ![][3]
8. Klik op **Opslaan**. Kopieer de **Client-ID** voor de app. Configureert u uw toepassing voor dit later gebruik.
9. Klik in de opdrachtbalk onder **eindpunten weergeven**, en kopieer de **Document met federatieve metagegevens** URL en downloaden van een document of navigeer naar deze in een browser.
10. Binnen de hoofdmap **EntityDescriptor** element, moet er een **id van de entiteit** kenmerk van het formulier `https://sts.windows.net/` gevolgd door een specifieke GUID voor uw tenant (een 'tenant-ID' genoemd). Deze waarde voor kopiëren - fungeren als uw **URL-verlener**. Configureert u uw toepassing voor dit later gebruik.

### <a name="secrets"></a>Toevoegen Azure Active Directory-informatie voor uw toepassing
1. Terug in de [Azure-portal], gaat u naar uw toepassing. Klik op **instellingen**, en vervolgens **verificatie/autorisatie**.
2. Als de verificatie/autorisatie-functie niet is ingeschakeld, schakelt u de schakeloptie voor **op**.
3. Klik op **Azure Active Directory**, en klik vervolgens op **Geavanceerd** onder **beheermodus**. Plak in het Client-ID en URL-verlener waarde die u eerder hebt verkregen. Klik vervolgens op **OK**.
   
   ![][1]
   
   Standaard-App Service biedt verificatie maar wordt niet geautoriseerde toegang beperkt tot uw site-inhoud en API's. U moet gebruikers machtigen in uw app-code.
4. (Optioneel) Instellen om toegang te beperken tot uw site tot alleen gebruikers die zijn geverifieerd door Azure Active Directory, **te ondernemen actie wanneer de aanvraag is niet geverifieerd** naar **aanmelden met Azure Active Directory**. Dit vereist dat alle aanvragen worden geverifieerd en alle niet-geverifieerde aanvragen worden omgeleid naar Azure Active Directory voor verificatie.
5. Klik op **Opslaan**.

U bent nu klaar voor gebruik van Azure Active Directory voor verificatie in uw app.

## <a name="optional-configure-a-native-client-application"></a>(Optioneel) Een systeemeigen clienttoepassing configureren
Azure Active Directory kunt u ook systeemeigen clients registreren die biedt meer controle over de machtigingen toewijzen. U moet dit als u wilt uitvoeren aanmeldingen met een bibliotheek, zoals de **Active Directory Authentication Library**.

1. Navigeer naar **Active Directory** in de [klassieke Azure-portal].
2. Selecteer uw directory en selecteer vervolgens de **toepassingen** boven op het tabblad. Klik op **toevoegen** onder een nieuwe app-registratie maken.
3. Klik op **mijn organisatie ontwikkelt toepassing toevoegen**.
4. Voer in de Wizard toepassing toevoegen, een **naam** voor uw toepassing en klik op de **systeemeigen clienttoepassing** type. Klik vervolgens op om door te gaan.
5. In de **omleidings-URI** Voer van uw site */.auth/login/done* eindpunt, met behulp van het HTTPS-schema. Deze waarde moet er ongeveer als *https://contoso.azurewebsites.net/.auth/login/done*. Als een Windows-toepassing maakt in plaats daarvan gebruikt de [pakket-SID](app-service-mobile-dotnet-how-to-use-client-library.md#package-sid) als de URI.
6. Wanneer de systeemeigen toepassing is toegevoegd, klikt u op de **configureren** tabblad. Zoek de **Client-ID** en noteer deze waarde.
7. Blader omlaag naar de **machtigingen voor andere toepassingen** sectie en klik op **toepassing toevoegen**.
8. Zoek de webtoepassing die u eerder hebt geregistreerd en klik op het plusteken. Klik vervolgens op het selectievakje om het dialoogvenster te sluiten. Als de webtoepassing niet kan worden gevonden, gaat u naar de registratie en een nieuwe antwoord-URL (bijv, de HTTP-versie van de huidige URL) toevoegen, klikt u op Opslaan en Herhaal deze stappen: de toepassing weergegeven in de lijst.
9. Open op het nieuwe item dat u zojuist hebt toegevoegd, de **gedelegeerde machtigingen** vervolgkeuzelijst en selecteer **toegang (appName)**. Klik vervolgens op **Opslaan**.

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
