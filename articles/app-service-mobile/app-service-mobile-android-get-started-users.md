---
title: aaaAdd verificatie op Android met Mobile Apps | Microsoft Docs
description: Meer informatie over hoe toouse Hallo functie Mobile Apps van Azure App Service tooauthenticate gebruikers van uw Android-app via een groot aantal identiteitsproviders, waaronder Google, Facebook, Twitter en Microsoft.
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 01f608f996c931c643790ed2778df11cf590c903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-android-app"></a>Verificatie tooyour Android-app toevoegen
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>Samenvatting
In deze zelfstudie maakt toevoegen u verificatie toohello todolist Quick Start-project op Android met behulp van een ondersteunde id-provider. Deze zelfstudie is gebaseerd op Hallo [aan de slag met Mobile Apps] zelfstudie die u moet eerst te voltooien.

## <a name="register"></a>Uw app registreren voor verificatie en Azure App Service configureren
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Uw app toohello toegestane externe Omleidings-URL's toevoegen

Veilige verificatie vereist dat u een nieuwe URL-schema voor uw app definiëren. Hierdoor Hallo verificatie system tooredirect back tooyour app zodra de Hallo verificatieproces is voltooid. In deze zelfstudie gebruiken we Hallo URL-schema _appname_ in. U kunt echter een URL-schema dat u kiest. Deze moet uniek tooyour mobiele toepassing. Hallo-omleiding tooenable aan serverzijde Hallo:

1. Selecteer in de Hallo [Azure portal], uw App Service.

2. Klik op Hallo **verificatie / autorisatie** menuoptie.

3. In Hallo **toegestaan externe Omleidings-URL's**, voer `appname://easyauth.callback`.  Hallo _appname_ in deze reeks is Hallo URL-schema voor uw mobiele toepassing.  Deze moet voldoen aan de normale URL-specificatie voor een protocol (Gebruik letters en cijfers alleen en begin met een letter).  U moet een notitie van Hallo-tekenreeks die u kiest, want u tooadjust uw code mobiele toepassing Hello URL-schema op verschillende plaatsen moet.

4. Klik op **OK**.

5. Klik op **Opslaan**.

## <a name="permissions"></a>Machtigingen tooauthenticated gebruikers beperken
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* In Android Studio, opent u het Hallo-project u voltooid met Hallo zelfstudie [aan de slag met Mobile Apps]. Van Hallo **uitvoeren** menu, klikt u op **app uitvoeren**, en controleer of dat een niet-verwerkte uitzondering met een statuscode van 401 (niet-geautoriseerd) treedt op nadat het Hallo-app wordt gestart.

     Deze uitzondering komt doordat Hallo app pogingen tooaccess Hallo terug als een niet-geverifieerde gebruiker beëindigen, maar Hallo *TodoItem* tabel nu is verificatie vereist.

Werk vervolgens Hallo app tooauthenticate gebruikers voordat u resources van Hallo die Mobile Apps back-end. 

## <a name="add-authentication-toohello-app"></a>Verificatie toohello app toevoegen
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <a name="cache-tokens"></a>Cache verificatietokens op Hallo-client
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a>Volgende stappen
Nu dat u deze basisverificatie-zelfstudie hebt voltooid, kunt u overwegen tooone Hallo volgende zelfstudies verder te gaan:

* [Push tooyour Android-app-meldingen toevoegen](app-service-mobile-android-get-started-push.md).
  Meer informatie over hoe uw Mobile Apps back tooconfigure toouse Azure notification hubs toosend-pushmeldingen eindigen.
* [Offlinesynchronisatie voor uw Android-app inschakelen](app-service-mobile-android-get-started-offline-data.md).
  Meer informatie over hoe de offline tooadd tooyour app met behulp van een back-end van Mobile Apps ondersteunen. Met het offline synchroniseren gebruikers kunnen communiceren met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding.

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[aan de slag met Mobile Apps]: app-service-mobile-android-get-started.md
