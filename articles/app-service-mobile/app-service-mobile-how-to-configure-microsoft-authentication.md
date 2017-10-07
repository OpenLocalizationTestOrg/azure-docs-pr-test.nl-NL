---
title: aaaHow tooconfigure Microsoft-Account verificatie voor uw toepassing App Services
description: Meer informatie over hoe tooconfigure Microsoft-Account verificatie voor uw App Services-toepassing.
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a>Hoe tooconfigure uw App Service-toepassing toouse-aanmelding met Microsoft-Account
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Dit onderwerp leest u hoe tooconfigure Azure App Service toouse Microsoft-Account als een verificatieprovider. 

## <a name="register-microsoft-account"></a>Uw app registreren bij Microsoft-Account
1. Meld u aan toohello [Azure-portal], en ga tooyour toepassing. Kopieer uw **URL**, die u later gebruiken tooconfigure uw app met Microsoft-Account.
2. Navigeer toohello [mijn toepassingen] pagina in de Microsoft-Account Developer Center Hallo en meld u aan met uw Microsoft-account, indien nodig.
3. Klik op **een app toevoegen**vervolgens typt u de naam van een toepassing en klik op **-toepassing maken**.
4. Maak een notitie van Hallo **toepassings-ID**, zoals u deze later hebt. 
5. Klik onder 'Platforms,' op **toevoegen Platform** en selecteert u 'Web'.
6. Klik onder 'Omleidings-URI' levering Hallo eindpunt voor uw toepassing, **opslaan**. 
   
   > [!NOTE]
   > De omleidings-URI Hallo-URL van uw toepassing toegevoegd aan de Hallo pad is, */.auth/login/microsoftaccount/callback*. Bijvoorbeeld `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.   
   > Zorg ervoor dat u van Hallo HTTPS-schema gebruikmaakt.
   
7. Klik onder 'Toepassing geheimen,' op **nieuw wachtwoord genereren**. Noteer Hallo-waarde die wordt weergegeven. Zodra u Hallo pagina verlaat, wordt deze niet opnieuw worden weergegeven.

    > [!IMPORTANT]
    > Hallo-wachtwoord is een belangrijke beveiligingsreferentie. Hallo-wachtwoord met anderen delen of deze te distribueren vanuit een clienttoepassing niet.

## <a name="secrets"></a>Microsoft-Account toevoegen informatie tooyour App Service-toepassing
1. Terug in Hallo [Azure-portal], tooyour toepassing navigeren, klik op **instellingen** > **verificatie / autorisatie**.
2. Als Hallo verificatie / autorisatie-functie is niet ingeschakeld, schakel deze **op**.
3. Klik op **Microsoft-Account**. Plak in Hallo toepassings-ID en wachtwoord waarden die u eerder hebt verkregen en optioneel in staat alle scopes die vereist zijn voor uw toepassing. Klik vervolgens op **OK**.
   
    ![][1]
   
    Standaard-App Service biedt verificatie maar niet beperkt geautoriseerde toegang tooyour site-inhoud en API's. U moet gebruikers machtigen in uw app-code.
4. (Optioneel) toorestrict toegang tooyour site tooonly gebruikers zijn geverifieerd door de Microsoft-account ingesteld **tootake actie wanneer de aanvraag is niet geverifieerd** te**Microsoft-Account**. Dit is vereist dat alle aanvragen worden geverifieerd en alle niet-geverifieerde aanvragen worden omgeleid tooMicrosoft-account voor verificatie.
5. Klik op **Opslaan**.

U bent nu klaar toouse Microsoft-Account voor verificatie in uw app.

## <a name="related-content"></a>Verwante inhoud
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[mijn toepassingen]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Azure-portal]: https://portal.azure.com/
