---
title: aaaAdd verificatie op Apache Cordova met Mobile Apps | Microsoft Docs
description: Meer informatie over hoe toouse Mobile Apps in Azure App Service tooauthenticate gebruikers van uw Apache Cordova-app via een groot aantal identiteitsproviders, waaronder Google, Facebook, Twitter en Microsoft.
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a>Verificatie tooyour Apache Cordova-app toevoegen
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>Samenvatting
In deze zelfstudie kunt u verificatie toohello todolist Quick Start-project toevoegen op Apache Cordova met behulp van een ondersteunde id-provider. Deze zelfstudie is gebaseerd op Hallo [aan de slag met Mobile Apps] zelfstudie die u moet eerst te voltooien.

## <a name="register"></a>Uw app registreren voor verificatie en Hallo App Service configureren
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[Bekijk een video van vergelijkbare stappen](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <a name="permissions"></a>Machtigingen tooauthenticated gebruikers beperken
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

U kunt nu controleren dat die back-end voor anonieme toegang tooyour is uitgeschakeld. In Visual Studio:

* Open Hallo-project dat u hebt gemaakt toen u Hallo-zelfstudie voltooid [aan de slag met Mobile Apps].
* Uw toepassing uitvoeren in Hallo **Google Android-Emulator**.
* Controleer of er een onverwachte fout in de verbinding wordt weergegeven nadat Hallo app is gestart.

Werk vervolgens Hallo app tooauthenticate gebruikers voordat u resources van Hallo-end voor mobiele App.

## <a name="add-authentication"></a>Verificatie toohello app toevoegen
1. Open het project in **Visual Studio**, open vervolgens Hallo `www/index.html` bestand voor bewerken.
2. Zoek Hallo `Content-Security-Policy` meta-code in Hallo head-sectie.  Hallo OAuth host toohello lijst van toegestane bronnen toevoegen.

   | Provider | De naam van de SDK-Provider | OAuth-Host |
   |:--- |:--- |:--- |
   | Azure Active Directory | AAD | https://login.microsoftonline.com |
   | Facebook | Facebook | https://www.Facebook.com |
   | Google | Google | https://accounts.Google.com |
   | Microsoft | MicrosoftAccount | https://login.live.com |
   | Twitter | Twitter | https://API.Twitter.com |

    Een voorbeeld van de inhoud-Security-beleid (toegepast voor Azure Active Directory) is als volgt:

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    Vervang `https://login.microsoftonline.com` met OAuth host Hallo Hallo voorafgaand aan de tabel.  Zie voor meer informatie over Hallo inhoud beveiligingsbeleid metatag Hallo [inhoud beveiligingsbeleid documentatie].

    Sommige verificatieproviders vereisen geen dat inhoud beveiligingsbeleid wijzigingen bij op de juiste mobiele apparaten.  Er zijn geen inhoud beveiligingsbeleid wijzigingen zijn vereist met Google-verificatie op een Android-apparaat.

3. Open Hallo `www/js/index.js` voor het bewerken van het bestand, zoek Hallo `onDeviceReady()` methode, en onder Hallo client maken code toe te voegen Hallo code te volgen:

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    Deze code vervangt de bestaande code Hallo die Hallo tabelverwijzing maakt en Hallo UI vernieuwt.

    verificatie begint Hallo login() methode met het Hallo-provider. Hallo login() methode is een async-functie die een JavaScript-belofte retourneert.  Hallo rest van de initialisatie van de Hallo wordt geplaatst in het antwoord van de belofte Hallo zodat deze wordt niet uitgevoerd totdat Hallo login() methode is voltooid.

4. Vervang in Hallo-code die u zojuist hebt toegevoegd, `SDK_Provider_Name` met Hallo-naam van uw aanmeldingsprovider. Bijvoorbeeld: voor Azure Active Directory, gebruiken `client.login('aad')`.
5. Voer uw project.  Wanneer het Hallo-project is geïnitialiseerd, ziet u uw toepassing hello OAuth-aanmeldingspagina voor Hallo verificatieprovider gekozen.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie [over verificatie] met Azure App Service.
* Hallo-zelfstudie gaan door toe te voegen [Pushmeldingen] tooyour Apache Cordova-app.

Meer informatie over hoe toouse Hallo SDK's.

* [Apache Cordova SDK]
* [ASP.NET Server SDK]
* [Node.js Server SDK]

<!-- URLs. -->
[aan de slag met Mobile Apps]: app-service-mobile-cordova-get-started.md
[inhoud beveiligingsbeleid documentatie]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[Pushmeldingen]: app-service-mobile-cordova-get-started-push.md
[over verificatie]: app-service-mobile-auth.md
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
