---
title: aaaHow tooconfigure Twitter-verificatie voor uw toepassing App Services
description: Meer informatie over hoe tooconfigure Twitter-verificatie voor uw App Services-toepassing.
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a>Hoe tooconfigure uw App Service-toepassing toouse Twitter-aanmelding
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Dit onderwerp leest u hoe tooconfigure Azure App Service toouse Twitter als een verificatieprovider.

toocomplete Hallo-procedure in dit onderwerp, moet u een Twitter-account met een geverifieerde e-mailadres en telefoonnummer nummer hebben. toocreate een nieuw Twitter-account, gaat u te<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.

## <a name="register"></a>Uw toepassing registreren met Twitter
1. Meld u aan toohello [Azure-portal], en ga tooyour toepassing. Kopieer uw **URL**. U gebruikt deze tooconfigure uw Twitter-app.
2. Navigeer toohello [Twitter ontwikkelaars] website, meld u aan met de referenties van uw Twitter-account en klikt u op **nieuwe App maken**.
3. Type in Hallo **naam** en een **beschrijving** voor uw nieuwe app. Plakken in uw toepassing **URL** voor Hallo **Website** waarde. Klik vervolgens voor Hallo **retouraanroep URL**, Hallo plakken **retouraanroep URL** u eerder hebt gekopieerd. Dit is de gateway van uw mobiele App toegevoegd aan de Hallo pad, */.auth/login/twitter/callback*. Bijvoorbeeld `https://contoso.azurewebsites.net/.auth/login/twitter/callback`. Zorg ervoor dat u van Hallo HTTPS-schema gebruikmaakt.
4. Op de pagina voor Hallo onder hello, lees en accepteer Hallo voorwaarden. Klik vervolgens op **uw Twitter-toepassing maken**. Deze registers Hallo app weergegeven Hallo Toepassingdetails.
5. Klik op Hallo **instellingen** tabblad selectievakje **toestaan dat deze toepassing gebruikt toobe toosign met Twitter**, klikt u vervolgens op **Update-instellingen**.
6. Selecteer Hallo **sleutels en toegangstokens** tabblad. Maak een notitie van Hallo waarden van **Consumer-sleutel (API-sleutel)** en **consumentgeheim (API geheim)**.
   
   > [!NOTE]
   > Hallo consumer geheime sleutel is een belangrijke beveiligingsreferentie. Geen dit geheim met anderen delen of deze met uw app te distribueren.
   > 
   > 

## <a name="secrets"></a>Informatie tooyour-toepassing toevoegen Twitter
1. Terug in Hallo [Azure-portal], tooyour toepassing navigeren. Klik op **instellingen**, en vervolgens **verificatie / autorisatie**.
2. Als Hallo verificatie / autorisatie-functie niet is ingeschakeld, schakelt u Hallo switch te**op**.
3. Klik op **Twitter**. Plak in Hallo App-ID en App-geheim waarden die u eerder hebt verkregen. Klik vervolgens op **OK**.
   
   ![][1]
   
   Standaard-App Service biedt verificatie maar niet beperkt geautoriseerde toegang tooyour site-inhoud en API's. U moet gebruikers machtigen in uw app-code.
4. (Optioneel) toorestrict toegang tooyour site tooonly gebruikers zijn geverifieerd door Twitter, ingesteld **tootake actie wanneer de aanvraag is niet geverifieerd** te**Twitter**. Dit vereist dat alle aanvragen worden geverifieerd en alle niet-geverifieerde aanvragen worden omgeleid tooTwitter voor verificatie.
5. Klik op **Opslaan**.

U bent nu klaar toouse Twitter voor verificatie in uw app.

## <a name="related-content"></a>Verwante inhoud
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[Twitter ontwikkelaars]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[Azure-portal]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
