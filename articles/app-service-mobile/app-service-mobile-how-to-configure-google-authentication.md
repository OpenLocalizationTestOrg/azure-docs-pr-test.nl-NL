---
title: aaaHow tooconfigure Google-verificatie voor uw toepassing App Services
description: Meer informatie over hoe tooconfigure Google-verificatie voor uw App Services-toepassing.
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a>Hoe tooconfigure uw App Service-toepassing toouse Google aanmelding
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Dit onderwerp leest u hoe tooconfigure Azure App Service toouse Google als een verificatieprovider.

toocomplete Hallo-procedure in dit onderwerp, moet u een Google-account met een geverifieerde e-mailadres hebben. toocreate een nieuw Google-account, gaat u te[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).

## <a name="register"></a>Uw toepassing registreren met Google
1. Meld u aan toohello [Azure-portal], en ga tooyour toepassing. Kopieer uw **URL**, die u later tooconfigure uw Google-app gebruiken.
2. Navigeer toohello [Google API's](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, meld u aan met de referenties van uw Google-account, klikt u op **Project maken**, bieden een **projectnaam**, klikt u vervolgens op  **Maak**.
3. Onder **sociale API's** klikt u op **Google + API** en vervolgens **inschakelen**.
4. In de linkernavigatiebalk, Hallo **referenties** > **OAuth toestemming scherm**, selecteer vervolgens uw **e-mailadres**, voer een **Productnaam**, en klik op **opslaan**.
5. In Hallo **referenties** tabblad **referenties maken** > **OAuth-Clientidentiteit**, selecteer daarna **webtoepassing**.
6. Plakken Hallo App Service **URL** u eerder hebt gekopieerd in **geautoriseerd JavaScript oorsprongen**, plak uw redirect URI in **omleidings-URI is gemachtigd**. Omleidings-URI Hallo-URL van uw toepassing met het Hallo-pad toegevoegd is Hallo */.auth/login/google/callback*. Bijvoorbeeld `https://contoso.azurewebsites.net/.auth/login/google/callback`. Zorg ervoor dat u van Hallo HTTPS-schema gebruikmaakt. Klik vervolgens op **Maken**.
7. Op het volgende scherm hello, noteer Hallo waarden van Hallo client-ID en client geheim.

    > [!IMPORTANT]
    > Hallo clientgeheim is een belangrijke beveiligingsreferentie. Dit geheim met anderen delen of deze te distribueren vanuit een clienttoepassing niet.


## <a name="secrets"></a>Toevoegen Google informatie tooyour toepassing
1. Terug in Hallo [Azure-portal], tooyour toepassing navigeren. Klik op **instellingen**, en vervolgens **verificatie / autorisatie**.
2. Als Hallo verificatie / autorisatie-functie niet is ingeschakeld, schakelt u Hallo switch te**op**.
3. Klik op **Google**. Plak in Hallo App-ID en App-geheim waarden die u eerder hebt verkregen en optioneel in staat alle scopes die vereist zijn voor uw toepassing. Klik vervolgens op **OK**.
   
   ![][1]
   
   Standaard-App Service biedt verificatie maar niet beperkt geautoriseerde toegang tooyour site-inhoud en API's. U moet gebruikers machtigen in uw app-code.
4. (Optioneel) toorestrict toegang tooyour site tooonly gebruikers zijn geverifieerd door Google en ingesteld **tootake actie wanneer de aanvraag is niet geverifieerd** te**Google**. Dit vereist dat alle aanvragen worden geverifieerd en alle niet-geverifieerde aanvragen worden omgeleid tooGoogle voor verificatie.
5. Klik op **Opslaan**.

U bent nu klaar toouse Google voor verificatie in uw app.

## <a name="related-content"></a>Verwante inhoud
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[Azure-portal]: https://portal.azure.com/

