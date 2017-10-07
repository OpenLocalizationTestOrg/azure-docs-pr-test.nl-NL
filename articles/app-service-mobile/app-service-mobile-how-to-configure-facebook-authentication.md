---
title: aaaHow tooconfigure Facebook-verificatie voor uw toepassing App Services
description: Meer informatie over hoe tooconfigure Facebook-verificatie voor uw App Services-toepassing.
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a>Hoe tooconfigure uw App Service-toepassing toouse Facebook-aanmelding
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Dit onderwerp leest u hoe tooconfigure Azure App Service toouse Facebook als een verificatieprovider.

toocomplete Hallo-procedure in dit onderwerp, moet u een Facebook-account met een geverifieerde e-mailadres en een mobiel telefoonnummer hebben. toocreate een nieuwe Facebook-account, gaat u te[facebook.com].

## <a name="register"></a>Uw toepassing registreren met Facebook
1. Meld u aan toohello [Azure-portal], en ga tooyour toepassing. Kopieer uw **URL**. U gebruikt deze tooconfigure uw Facebook-app.
2. Navigeer in een ander browservenster toohello [Facebook-ontwikkelaars] website en aanmelden met uw Facebook-accountreferenties.
3. (Optioneel) Als u nog niet hebt geregistreerd, klikt u op **Apps** > **registreren als een ontwikkelaar**, accepteert u Hallo beleid en registratie van Hallo stappen.
4. Klik op **mijn Apps** > **toevoegen van een nieuwe App** > **Website** > **overslaan en App-ID maken**. 
5. In **weergavenaam**, typ een unieke naam voor uw app, type uw **Neem contact op met E-mail**, kies een **categorie** voor uw app, klik vervolgens op **App-ID maken**en Hallo beveiligingscontrole te voltooien. Hiermee gaat u toohello dashboard voor ontwikkelaars voor uw nieuwe Facebook-app.
6. Klik onder 'Facebook aanmelding,' op **aan de slag**. Toevoegen van uw toepassing **omleidings-URI** te**geldig OAuth omleidings-URI's**, klikt u vervolgens op **wijzigingen opslaan**. 
   
   > [!NOTE]
   > De omleidings-URI Hallo-URL van uw toepassing toegevoegd aan de Hallo pad is, */.auth/login/facebook/callback*. Bijvoorbeeld `https://contoso.azurewebsites.net/.auth/login/facebook/callback`. Zorg ervoor dat u van Hallo HTTPS-schema gebruikmaakt.
   > 
   > 
7. Klik in de linkernavigatiebalk hello, **instellingen**. Op Hallo **App geheim** veld, klikt u op **weergeven**, geeft u uw wachtwoord als aangevraagd, maak een notitie van waarden van Hallo **App-ID** en **App geheim**. U gebruikt deze later tooconfigure uw toepassing in Azure.
   
   > [!IMPORTANT]
   > Hallo app geheime sleutel is een belangrijke beveiligingsreferentie. Dit geheim met anderen delen of deze te distribueren vanuit een clienttoepassing niet.
   > 
   > 
8. Hallo Facebook-account dat gebruikt tooregister Hallo toepassing is is een beheerder van Hallo-app. Alleen beheerders kunnen op dit moment aanmelden bij deze toepassing. tooauthenticate andere accounts Facebook, klikt u op **App revisie** en schakel **maken < uw app-naam > openbare** tooenable algemene openbare toegang met Facebook-verificatie.

## <a name="secrets"></a>Toevoegen Facebook informatie tooyour-toepassing
1. Terug in Hallo [Azure-portal], tooyour toepassing navigeren. Klik op **instellingen** > **verificatie / autorisatie**, en zorg ervoor dat **verificatie van App Service** is **op**.
2. Klik op **Facebook**, plak in Hallo App-ID en App-geheim waarden die u eerder hebt verkregen, eventueel alle scopes die nodig is voor uw toepassing inschakelen en klik vervolgens op **OK**.
   
    ![][0]
   
    Standaard-App Service biedt verificatie maar niet beperkt geautoriseerde toegang tooyour site-inhoud en API's. U moet gebruikers machtigen in uw app-code.
3. (Optioneel) toorestrict toegang tooyour site tooonly gebruikers zijn geverifieerd door Facebook, ingesteld **tootake actie wanneer de aanvraag is niet geverifieerd** te**Facebook**. Dit vereist dat alle aanvragen worden geverifieerd en alle niet-geverifieerde aanvragen worden omgeleid tooFacebook voor verificatie.
4. Wanneer u klaar verificatie configureren, klikt u op **opslaan**.

U bent nu klaar toouse Facebook voor verificatie in uw app.

## <a name="related-content"></a>Verwante inhoud
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[Facebook-ontwikkelaars]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[Azure-portal]: https://portal.azure.com/
