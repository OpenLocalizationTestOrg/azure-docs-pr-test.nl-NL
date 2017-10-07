---
title: aaaGet gestart met verificatie voor mobiele Apps in app voor Xamarin Forms | Microsoft Docs
description: Meer informatie over hoe toouse Mobile Apps tooauthenticate gebruikers van uw app Xamarin Forms via een groot aantal identiteitsproviders, waaronder AAD, Google, Facebook, Twitter en Microsoft.
services: app-service\mobile
documentationcenter: xamarin
author: panarasi
manager: syntaxc4
editor: 
ms.assetid: 9c55e192-c761-4ff2-8d88-72260e9f6179
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: panarasi
ms.openlocfilehash: 7f6716619f33d9cc4f866c41effba8f048dc49fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarin-forms-app"></a>Verificatie tooyour Xamarin Forms app toevoegen
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a>Overzicht
Dit onderwerp leest u hoe tooauthenticate gebruikers van een App Service Mobile App van uw clienttoepassing. In deze zelfstudie kunt u verificatie toevoegen aan Hallo Xamarin Forms Quick Start-project met behulp van een id-provider die wordt ondersteund door App Service. Nadat wordt is geverifieerd en geautoriseerd door uw mobiele App, Hallo gebruiker-id-waarde wordt weergegeven en kunt u zich tabelgegevens kunnen tooaccess beperkt.

## <a name="prerequisites"></a>Vereisten
Voor Hallo beste resultaat in deze zelfstudie, raden we u eerst Hallo voltooid [maken van een app voor Xamarin Forms] [ 1] zelfstudie. Nadat u deze zelfstudie hebt voltooid, hebt u een Xamarin Forms-project dat een TodoList-App voor meerdere platforms.

Als u geen gebruik Hallo snel starten-serverproject gedownload, moet u Hallo verificatie pakket tooyour extensieproject toevoegen. Zie voor meer informatie over server extensiepakketten [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps][2].

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>Uw app registreren voor verificatie en App-Services configureren
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Uw app toohello toegestane externe Omleidings-URL's toevoegen

Veilige verificatie vereist dat u een nieuwe URL-schema voor uw app definiëren. Hierdoor Hallo verificatie system tooredirect back tooyour app zodra de Hallo verificatieproces is voltooid. In deze zelfstudie gebruiken we Hallo URL-schema _appname_ in. U kunt echter een URL-schema dat u kiest. Deze moet uniek tooyour mobiele toepassing. Hallo-omleiding tooenable aan serverzijde Hallo:

1. Selecteer in de Hallo [Azure portal], uw App Service.

2. Klik op Hallo **verificatie / autorisatie** menuoptie.

3. In Hallo **toegestaan externe Omleidings-URL's**, voer `url_scheme_of_your_app://easyauth.callback`.  Hallo **url_scheme_of_your_app** in deze reeks is Hallo URL-schema voor uw mobiele toepassing.  Deze moet voldoen aan de normale URL-specificatie voor een protocol (Gebruik letters en cijfers alleen en begin met een letter).  U moet een notitie van Hallo-tekenreeks die u kiest, want u tooadjust uw code mobiele toepassing Hello URL-schema op verschillende plaatsen moet.

4. Klik op **OK**.

5. Klik op **Opslaan**.

## <a name="restrict-permissions-tooauthenticated-users"></a>Machtigingen tooauthenticated gebruikers beperken
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a>Verificatie toohello draagbare klassebibliotheek toevoegen
Hallo maakt gebruik van Mobile Apps [LoginAsync] [ 3] uitbreidingsmethode op Hallo [MobileServiceClient] [ 4] toosign in een gebruiker met App Service -verificatie. Dit voorbeeld wordt een beheerde server authenticatiestroom die wordt weergegeven van de provider Hallo aanmelden interface in Hallo app gebruikt. Zie voor meer informatie [authentication Server beheerd][5]. Voor een betere gebruikerservaring in uw productie-app, moet u rekening houden met gebruik van [Client beheerd verificatie][6].

tooauthenticate aan een project Xamarin Forms definiëren een **IAuthenticate** Hallo Portable Class Library voor Hallo app-interface. Voeg vervolgens een **aanmelden** knop toohello-gebruikersinterface is gedefinieerd in Hallo draagbare klassebibliotheek, die u op toostart verificatie. Gegevens worden geladen vanuit Hallo mobiele app back-end na een geslaagde authenticatie.

Implementeer Hallo **IAuthenticate** interface voor elk platform dat wordt ondersteund door uw app.

1. Open in Visual Studio of Xamarin Studio App.cs van Hallo-project met **draagbare** in naam van Hallo Portable Class Library-project is, voegt u Hallo volgende `using` instructie:

        using System.Threading.Tasks;
2. Voeg de volgende Hallo in App.cs, `IAuthenticate` interface definition direct vóór de Hallo `App` definitie van klasse.

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. tooinitialize hello interface met een implementatie platform-specifieke toevoegen na de statische leden toohello Hallo **App** klasse.

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. TodoList.xaml openen vanuit Hallo Portable Class Library-project, voeg de volgende Hallo **knop** -element in Hallo *buttonsPanel* lay-element na Hallo bestaande knop:

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    Deze knop activeert verificatie met uw mobiele app back-end server beheerd.
5. TodoList.xaml.cs openen vanuit Hallo Portable Class Library-project, voeg dan Hallo volgende veld toohello `TodoList` klasse:

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. Vervang Hallo **OnAppearing** methode Hello code te volgen:

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems tootrue in order toosynchronize hello data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide hello Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    Deze code zorgt ervoor dat de gegevens alleen vernieuwd van Hallo-service nadat u hebt geverifieerd.
7. Hallo-handler voor Hallo na toevoegen **op wordt geklikt** gebeurtenis toohello **TodoList** klasse:

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. De wijzigingen opslaan en opnieuw opbouwen Hallo Portable Class Library project zonder fouten te controleren.

## <a name="add-authentication-toohello-android-app"></a>Verificatie toohello Android-app toevoegen
Deze sectie wordt beschreven hoe tooimplement hello **IAuthenticate** interface in Hallo Android-app-project. Deze sectie overslaan als Android-apparaten worden niet ondersteund.

1. In Visual Studio of Xamarin Studio, met de rechtermuisknop op Hallo **droid** project, klikt u vervolgens **instellen als opstartproject**.
2. Druk op F5 toostart Hallo project in Hallo foutopsporingsprogramma en controleer of dat een niet-verwerkte uitzondering met een statuscode van 401 (niet-geautoriseerd) treedt op nadat de app wordt gestart. Hallo 401 code wordt geproduceerd omdat beperkte tooauthorized gebruikers alleen toegang op Hallo back-end.
3. MainActivity.cs opent in Hallo Android-project en voeg de volgende Hallo `using` instructies:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. Update Hallo **MainActivity** klasse tooimplement hello **IAuthenticate** interface, als volgt:

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. Update Hallo **MainActivity** klasse door toe te voegen een **MobileServiceUser** veld en een **verifiëren** methode die wordt door Hallo vereist **IAuthenticate**  interface, als volgt:

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                user = await TodoItemManager.DefaultManager.CurrentClient.LoginAsync(this, 
                    MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                if (user != null)
                {
                    message = string.Format("you are now signed-in as {0}.",
                        user.UserId);
                    success = true;
                }
            }
            catch (Exception ex)
            {
                message = ex.Message;
            }

            // Display hello success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    Als u van een id-provider dan Facebook gebruikmaakt, kiest u een andere waarde voor [MobileServiceAuthenticationProvider][7].

6. Hallo-code in volgende toevoegen <application> knooppunt van AndroidManifest.xml:

```xml
    <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
      <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
      </intent-filter>
    </activity>
```

1. Hallo na code toohello toevoegen **OnCreate** methode Hallo **MainActivity** klasse vóór Hallo aanroep te`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    Deze code wordt ervoor gezorgd Hallo verificator wordt geïnitialiseerd voordat Hallo app geladen.
2. Hallo app opnieuw samenstellen, uitvoeren en meld u aan met de Hallo verificatieprovider u hebt gekozen en controleer of dat u kunt tooaccess gegevens als een geverifieerde gebruiker zijn.

## <a name="add-authentication-toohello-ios-app"></a>Verificatie toohello iOS-app toevoegen
Deze sectie wordt beschreven hoe tooimplement hello **IAuthenticate** interface in Hallo iOS-app-project. Deze sectie overslaan als iOS-apparaten worden niet ondersteund.

1. In Visual Studio of Xamarin Studio, met de rechtermuisknop op Hallo **iOS** project, klikt u vervolgens **instellen als opstartproject**.
2. Druk op F5 toostart Hallo project in Hallo foutopsporingsprogramma en controleer of dat een niet-verwerkte uitzondering met een statuscode van 401 (niet-geautoriseerd) treedt op nadat het Hallo-app wordt gestart. Hallo 401-respons wordt geproduceerd omdat beperkte tooauthorized gebruikers alleen toegang op Hallo back-end.
3. AppDelegate.cs opent in Hallo iOS-project en voeg de volgende Hallo `using` instructies:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. Update Hallo **AppDelegate** klasse tooimplement hello **IAuthenticate** interface, als volgt:

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. Update Hallo **AppDelegate** klasse door toe te voegen een **MobileServiceUser** veld en een **verifiëren** methode die wordt door Hallo vereist **IAuthenticate**  interface, als volgt:

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(UIApplication.SharedApplication.KeyWindow.RootViewController,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                        success = true;
                    }
                }
            }
            catch (Exception ex)
            {
               message = ex.Message;
            }

            // Display hello success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    Als u van een id-provider dan Facebook gebruikmaakt, kiest u een andere waarde voor [MobileServiceAuthenticationProvider].

6. Hallo AppDelegate klasse bijwerken door toe te voegen methode-overload OpenUrl (UIApplication NSUrl-url-app NSDictionary opties)

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. Toevoegen van de volgende regel code toohello hello **FinishedLaunching** te aanroep van servermethode voordat Hallo`LoadApplication()`:

        App.Init(this);

    Deze code wordt ervoor gezorgd Hallo verificator is geïnitialiseerd voordat de app hello wordt geladen.

6. Voeg **{url_scheme_of_your_app}** tooURL-schema's in de Info.plist.

7. Hallo app opnieuw samenstellen, uitvoeren en meld u aan met de Hallo verificatieprovider u hebt gekozen en controleer of dat u kunt tooaccess gegevens als een geverifieerde gebruiker zijn.

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a>Toevoegen van verificatie tooWindows 10 (inclusief Phone) app-projecten
Deze sectie wordt beschreven hoe tooimplement hello **IAuthenticate** interface in Hallo Windows 10-app-projecten. Hallo dezelfde stappen van toepassing op Universal Windows Platform (UWP)-projecten, maar het gebruik van Hallo **UWP** project (met vermelde wijzigingen). Deze sectie overslaan als Windows-apparaten worden niet ondersteund.

1. ' In Visual Studio met de rechtermuisknop op beide Hallo **UWP** project, klikt u vervolgens **instellen als opstartproject**.
2. Druk op F5 toostart Hallo project in Hallo foutopsporingsprogramma en controleer of dat een niet-verwerkte uitzondering met een statuscode van 401 (niet-geautoriseerd) treedt op nadat het Hallo-app wordt gestart. Hallo 401-respons gebeurt omdat beperkte tooauthorized gebruikers alleen toegang op Hallo back-end.
3. MainPage.xaml.cs open voor Hallo Windows app-project en voeg de volgende Hallo `using` instructies:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    Vervang `<your_Portable_Class_Library_namespace>` met Hallo naamruimte voor uw draagbare klassebibliotheek.
4. Update Hallo **MainPage** klasse tooimplement hello **IAuthenticate** interface, als volgt:

        public sealed partial class MainPage : IAuthenticate
5. Update Hallo **MainPage** klasse door toe te voegen een **MobileServiceUser** veld en een **verifiëren** methode die wordt door Hallo vereist **IAuthenticate** interface, als volgt:

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            string message = string.Empty;
            var success = false;

            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        success = true;
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                    }
                }

            }
            catch (Exception ex)
            {
                message = string.Format("Authentication Failed: {0}", ex.Message);
            }

            // Display hello success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    Als u van een id-provider dan Facebook gebruikmaakt, kiest u een andere waarde voor [MobileServiceAuthenticationProvider].

1. Toevoegen van de volgende coderegel in de constructor voor Hallo HALLO hallo **MainPage** klasse vóór Hallo aanroep te`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    Vervang `<your_Portable_Class_Library_namespace>` met Hallo naamruimte voor uw draagbare klassebibliotheek.

3. Als u **UWP**, voeg de volgende Hallo **OnActivated** methode overschrijven toohello **App** klasse:

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   Hallo methode overschrijven wanneer al bestaat, voorwaardelijke code Hallo van Hallo voorgaande codefragment toevoegen.  Deze code is niet vereist voor universele Windows-projecten.

3. Voeg **{url_scheme_of_your_app}** in Package.appxmanifest. 

4. Hallo app opnieuw samenstellen, uitvoeren en meld u aan met de Hallo verificatieprovider u hebt gekozen en controleer of dat u kunt tooaccess gegevens als een geverifieerde gebruiker zijn.

## <a name="next-steps"></a>Volgende stappen
Nu dat u deze basisverificatie-zelfstudie hebt voltooid, kunt u overwegen tooone Hallo volgende zelfstudies verder te gaan:

* [Push notifications tooyour app toevoegen](app-service-mobile-xamarin-forms-get-started-push.md)

  Informatie over hoe tooyour app ondersteuning bieden voor pushmeldingen tooadd en pushmeldingen voor uw mobiele App back-end toouse Azure Notification Hubs toosend configureren.
* [Offlinesynchronisatie voor uw app inschakelen](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  Meer informatie over hoe tooadd offline ondersteuning bieden voor uw app met een back-end voor de mobiele App. Offlinesynchronisatie kunnen eindgebruikers gebruikers toointeract met een mobiele app - weergeven, toevoegen of wijzigen van gegevens -, zelfs wanneer er geen netwerkverbinding.

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
