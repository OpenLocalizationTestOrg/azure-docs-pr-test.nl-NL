---
title: aaaGet gestart met verificatie voor mobiele Apps in Xamarin Android
description: Meer informatie over hoe toouse Mobile Apps tooauthenticate gebruikers van uw Xamarin.android-app via een groot aantal identiteitsproviders, waaronder AAD, Google, Facebook, Twitter en Microsoft.
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 570fc12b-46a9-4722-b2e0-0d1c45fb2152
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: 500a4efa816e4f6d75d359e31d6357da56a72f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinandroid-app"></a>Verificatie tooyour Xamarin.Android-app toevoegen
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Dit onderwerp leest u hoe tooauthenticate gebruikers van een mobiele App van uw clienttoepassing. In deze zelfstudie maakt toevoegen u verificatie toohello Quick Start-project met behulp van een id-provider die wordt ondersteund door Azure Mobile Apps. Nadat wordt hebt geverifieerd en gemachtigd in Hallo mobiele App, wordt Hallo gebruiker-ID-waarde weergegeven.

Deze zelfstudie is gebaseerd op Hallo mobiele App Quick Start. U moet ook eerst Hallo-zelfstudie hebt voltooid [een Xamarin.Android-app maken]. Als u geen gebruik Hallo snel starten-serverproject gedownload, moet u Hallo verificatie pakket tooyour extensieproject toevoegen. Zie voor meer informatie over server extensiepakketten [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="register"></a>Uw app registreren voor verificatie en App-Services configureren
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Uw app toohello toegestane externe Omleidings-URL's toevoegen

Veilige verificatie vereist dat u een nieuwe URL-schema voor uw app definiëren. Hierdoor Hallo verificatie system tooredirect back tooyour app zodra de Hallo verificatieproces is voltooid. In deze zelfstudie gebruiken we Hallo URL-schema _appname_ in. U kunt echter een URL-schema dat u kiest. Deze moet uniek tooyour mobiele toepassing. Hallo-omleiding tooenable aan serverzijde Hallo:

1. Selecteer in de Hallo [Azure portal], uw App Service.

2. Klik op Hallo **verificatie / autorisatie** menuoptie.

3. In Hallo **toegestaan externe Omleidings-URL's**, voer `url_scheme_of_your_app://easyauth.callback`.  Hallo **url_scheme_of_your_app** in deze reeks is Hallo URL-schema voor uw mobiele toepassing.  Deze moet voldoen aan de normale URL-specificatie voor een protocol (Gebruik letters en cijfers alleen en begin met een letter).  U moet een notitie van Hallo-tekenreeks die u kiest, want u tooadjust uw code mobiele toepassing Hello URL-schema op verschillende plaatsen moet.

4. Klik op **OK**.

5. Klik op **Opslaan**.

## <a name="permissions"></a>Machtigingen tooauthenticated gebruikers beperken
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

Voer Hallo client-project op een apparaat of emulator in Visual Studio en Xamarin Studio. Controleer of dat een niet-verwerkte uitzondering met een statuscode van 401 (niet-geautoriseerd) treedt op nadat het Hallo-app wordt gestart. Dit gebeurt omdat Hallo app tooaccess backend voor mobiele Apps als een niet-geverifieerde gebruiker probeert. Hallo *TodoItem* tabel nu is verificatie vereist.

Vervolgens wordt u Hallo client app toorequest resources uit de back-end van Hallo Mobile Apps bijwerken met een geverifieerde gebruiker.

## <a name="add-authentication"></a>Verificatie toohello app toevoegen
Hallo-app is een bijgewerkte toorequire gebruikers tootap hello **aanmelden** knop en worden geverifieerd voordat gegevens worden weergegeven.

1. Hallo na code toohello toevoegen **TodoActivity** klasse:
   
        // Define a authenticated user.
        private MobileServiceUser user;
        private async Task<bool> Authenticate()
        {
                var success = false;
                try
                {
                    // Sign in with Facebook login using a server-managed flow.
                    user = await client.LoginAsync(this,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    CreateAndShowDialog(string.Format("you are now logged in - {0}",
                        user.UserId), "Logged in!");
   
                    success = true;
                }
                catch (Exception ex)
                {
                    CreateAndShowDialog(ex, "Authentication failed");
                }
                return success;
        }
   
        [Java.Interop.Export()]
        public async void LoginUser(View view)
        {
            // Load data only after authentication succeeds.
            if (await Authenticate())
            {
                //Hide hello button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load hello data.
                OnRefreshItemsSelected();
            }
        }
   
    Hiermee maakt u een nieuwe methode tooauthenticate een gebruiker en een methode-handler voor een nieuwe **aanmelden** knop. Hallo-gebruiker in bovenstaande Hallo voorbeeldcode wordt geverifieerd met behulp van een Facebook-aanmelding. Gebruikte toodisplay Hallo gebruikers-ID eenmaal is geverifieerd, is een dialoogvenster.
   
   > [!NOTE]
   > Als u van een id-provider dan Facebook gebruikmaakt, Hallo-waarde doorgegeven te wijzigen**LoginAsync** hierboven tooone van de volgende Hallo: *MicrosoftAccount*, *Twitter*, *Google*, of *WindowsAzureActiveDirectory*.
   > 
   > 
2. In Hallo **OnCreate** methode, verwijderen of commentarieer Hallo coderegel te volgen:
   
        OnRefreshItemsSelected ();
3. Voeg toe Hallo volgende Hallo Activity_To_Do.axml bestand *LoginUser* knop definitie voordat Hallo bestaande *AddItem* knop:
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. Hallo volgende element toohello Strings.xml resources toevoegen:
   
        <string name="login_button_text">Sign in</string>
5. Hallo AndroidManifest.xml bestand openen, toevoegen Hallo-code in volgende `<application>` XML-element:

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. In Visual Studio en Xamarin Studio Hallo client-project uitvoeren op een apparaat of emulator en meld u aan met uw gekozen id-provider. Wanneer u is aangemeld bent, Hallo app uw aanmeldings-ID wordt weergegeven en Hallo lijst met todo-items en u kunt updates toohello gegevens maken.

<!-- URLs. -->
[een Xamarin.Android-app maken]: app-service-mobile-xamarin-android-get-started.md