---
title: aaaGet gestart met verificatie voor mobiele Apps in Xamarin voor iOS
description: Meer informatie over hoe toouse Mobile Apps tooauthenticate gebruikers van uw Xamarin iOS-app via een groot aantal identiteitsproviders, waaronder AAD, Google, Facebook, Twitter en Microsoft.
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 180cc61b-19c5-48bf-a16c-7181aef3eacc
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: glenga
ms.openlocfilehash: 6458e9651b03df61c86b88b11953792e04bfa5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinios-app"></a>Verificatie tooyour Xamarin.iOS-app toevoegen
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Dit onderwerp leest u hoe tooauthenticate gebruikers van een App Service Mobile App van uw clienttoepassing. In deze zelfstudie voegt u verificatie toohello Xamarin.iOS Quick Start-project met behulp van een id-provider die wordt ondersteund door App Service. Nadat wordt is geverifieerd en geautoriseerd door uw mobiele App, Hallo gebruiker-ID-waarde wordt weergegeven en kunt u gegevens in een tabel staat tooaccess beperkt.

U moet eerst Hallo-zelfstudie hebt voltooid [een Xamarin.iOS-app maken]. Als u geen gebruik Hallo snel starten-serverproject gedownload, moet u Hallo verificatie pakket tooyour extensieproject toevoegen. Zie voor meer informatie over server extensiepakketten [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>Uw app registreren voor verificatie en App-Services configureren
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a>Uw app toohello toegestane externe Omleidings-URL's toevoegen

Veilige verificatie vereist dat u een nieuwe URL-schema voor uw app definiëren. Hierdoor Hallo verificatie system tooredirect back tooyour app zodra de Hallo verificatieproces is voltooid. In deze zelfstudie gebruiken we Hallo URL-schema _appname_ in. U kunt echter een URL-schema dat u kiest. Deze moet uniek tooyour mobiele toepassing. Hallo-omleiding tooenable aan serverzijde Hallo:

1. Selecteer in de Hallo [Azure portal], uw App Service.

2. Klik op Hallo **verificatie / autorisatie** menuoptie.

3. In Hallo **toegestaan externe Omleidings-URL's**, voer `url_scheme_of_your_app://easyauth.callback`.  Hallo **url_scheme_of_your_app** in deze reeks is Hallo URL-schema voor uw mobiele toepassing.  Deze moet voldoen aan de normale URL-specificatie voor een protocol (Gebruik letters en cijfers alleen en begin met een letter).  U moet een notitie van Hallo-tekenreeks die u kiest, want u tooadjust uw code mobiele toepassing Hello URL-schema op verschillende plaatsen moet.

4. Klik op **OK**.

5. Klik op **Opslaan**.

## <a name="restrict-permissions-tooauthenticated-users"></a>Machtigingen tooauthenticated gebruikers beperken
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

&nbsp;&nbsp;4. Voer Hallo client-project op een apparaat of emulator in Visual Studio en Xamarin Studio. Controleer of dat een niet-verwerkte uitzondering met een statuscode van 401 (niet-geautoriseerd) treedt op nadat het Hallo-app wordt gestart. Hallo mislukte is vastgelegd toohello console van Hallo foutopsporingsprogramma. Dus in Visual Studio ziet u fout in het uitvoervenster Hallo Hallo.

&nbsp;&nbsp;Deze onbevoegde fout treedt op omdat het Hallo-app probeert tooaccess backend voor mobiele Apps als een niet-geverifieerde gebruiker. Hallo *TodoItem* tabel nu is verificatie vereist.

Vervolgens wordt u Hallo client app toorequest resources uit de back-end van Hallo Mobile Apps bijwerken met een geverifieerde gebruiker.

## <a name="add-authentication-toohello-app"></a>Verificatie toohello app toevoegen
In deze sectie wijzigt u Hallo app toodisplay een aanmeldingsscherm voordat gegevens worden weergegeven. Wanneer Hallo-app wordt gestart, niet niet verbinding maakt tooyour App Service en gegevens kunnen niet worden weergegeven. Na de eerste keer Hallo voert die gebruiker Hallo gebaar voor het vernieuwen van Hallo Hallo aanmeldingsscherm wordt weergegeven; na een geslaagde aanmelding wordt hello lijst met todo-items weergegeven.

1. Open in Hallo clientproject Hallo-bestand **QSTodoService.cs** en voeg de volgende Hallo gebruiksinstructie en `MobileServiceUser` met accessor toohello QSTodoService klasse:
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. Met de naam van de nieuwe methode Add **verifiëren** te**QSTodoService** Hello definitie te volgen:

        public async Task Authenticate(UIViewController view)
        {
            try
            {
                AppDelegate.ResumeWithURL = url => url.Scheme == "zumoe2etestapp" && client.ResumeWithURL(url);
                user = await client.LoginAsync(view, MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine (@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
            }
        }

    >[AZURE.NOTE] Als u van een id-provider dan een Facebook gebruikmaakt, Hallo-waarde doorgegeven te wijzigen**LoginAsync** hierboven tooone van de volgende Hallo: _MicrosoftAccount_, _Twitter_, _Google_, of _WindowsAzureActiveDirectory_.

3. Open **QSTodoListViewController.cs**. Hallo-methodedefinitie van wijzigen **ViewDidLoad** Hallo aanroep te verwijderen**RefreshAsync()** bijna Hallo einde:
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out hello call tooRefreshAsync
            // await RefreshAsync();
        }
4. Hallo-methode Modify **RefreshAsync** tooauthenticate als hello **gebruiker** eigenschap is null. Hallo code Hallo boven aan het Hallo-methodedefinitie volgende toevoegen:
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. Open **AppDelegate.cs**, Hallo methode volgende toevoegen:

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. Open **Info.plist** bestand, te navigeren**URL typen** in Hallo **Geavanceerd** sectie. Nu configureren Hallo **id** en Hallo **URL-schema's** van uw URL-Type en klik op **URL-Type toevoegen**. **URL-schema's** moet dezelfde Hallo als uw {url_scheme_of_your_app}.
7. In Visual Studio of Xamarin Studio verbonden tooyour Xamarin bouwen Host op uw Mac Hallo clientproject die gericht is op een apparaat of emulator uitgevoerd. Controleer of u dat die app Hallo geen gegevens weergegeven.
   
    Hallo vernieuwen gebaar door binnen te halen omlaag Hallo lijst met items, waardoor de Hallo aanmelding scherm tooappear uitvoeren. Zodra u geldige referenties hebt, Hallo app Hallo-lijst van todo-items worden weergegeven en kunt u updates toohello gegevens maken.

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[een Xamarin.iOS-app maken]: app-service-mobile-xamarin-ios-get-started.md