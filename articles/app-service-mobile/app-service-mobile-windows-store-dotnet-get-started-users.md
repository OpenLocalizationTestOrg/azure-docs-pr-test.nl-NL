---
title: aaaAdd authentication tooyour Universal Windows Platform (UWP)-app | Microsoft Docs
description: 'Meer informatie over hoe toouse Azure App Service Mobile Apps tooauthenticate gebruikers van uw Universal Windows Platform (UWP)-app met een aantal identiteitsproviders, waaronder: AAD, Google, Facebook, Twitter en Microsoft.'
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: ad4477e9509f1c40c33e71818e268f6857fe1e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-windows-app"></a>Verificatie tooyour Windows-app toevoegen
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Dit onderwerp leest u hoe tooadd cloudverificatie tooyour mobiele app. In deze zelfstudie kunt u verificatie toohello Universal Windows Platform (UWP)-Quick Start-project toevoegen voor mobiele Apps met behulp van een id-provider die wordt ondersteund door Azure App Service. Na wordt is geverifieerd en gemachtigd door uw back-end voor de mobiele App, wordt Hallo gebruiker-ID-waarde weergegeven.

Deze zelfstudie is gebaseerd op Hallo Mobile Apps-Quick Start. U moet eerst Hallo-zelfstudie hebt voltooid [aan de slag met Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).

## <a name="register"></a>Uw app registreren voor verificatie en Hallo App Service configureren
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

U kunt nu controleren dat die back-end voor anonieme toegang tooyour is uitgeschakeld. Met de Hallo UWP-appproject instellen als opstartproject hello, implementeren en uitvoeren van Hallo app; Controleer of dat een niet-verwerkte uitzondering met een statuscode van 401 (niet-geautoriseerd) treedt op nadat het Hallo-app wordt gestart. Dit gebeurt omdat Hallo app probeert tooaccess op uw mobiele App-Code als een niet-geverifieerde gebruiker, maar Hallo *TodoItem* tabel nu is verificatie vereist.

Vervolgens wordt u Hallo app tooauthenticate gebruikers bijwerken voordat u resources van uw App Service.

## <a name="add-authentication"></a>Verificatie toohello app toevoegen
1. In de UWP-appproject Hallo bestand MainPage.xaml.cs en Hallo codefragment volgende toevoegen:
   
        // Define a member variable for storing hello signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs hello authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' toohello name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    Deze code verifieert Hallo-gebruiker met een Facebook-aanmelding. Als u van een id-provider dan Facebook gebruikmaakt, wijzigt u de waarde Hallo van **MobileServiceAuthenticationProvider** boven toohello waarde voor de provider.
2. Vervang Hallo **OnNavigatedTo()** methode in MainPage.xaml.cs. Vervolgens voegt u een **aanmelden** knop toohello app waarmee de verificatie wordt geactiveerd.

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. Hallo code codefragment toohello MainPage.xaml.cs volgende toevoegen:
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login hello user and then load data from hello mobile app.
            if (await AuthenticateAsync())
            {
                // Switch hello buttons and load items from hello mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. Hallo MainPage.xaml projectbestand openen, zoek naar Hallo-element waarmee wordt gedefinieerd Hallo **opslaan** knop en vervang deze door Hallo code te volgen:
   
        <Button Name="ButtonSave" Visibility="Collapsed" Margin="0,8,8,0" 
                Click="ButtonSave_Click">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Add"/>
                <TextBlock Margin="5">Save</TextBlock>
            </StackPanel>
        </Button>
        <Button Name="ButtonLogin" Visibility="Visible" Margin="0,8,8,0" 
                Click="ButtonLogin_Click" TabIndex="0">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Permissions"/>
                <TextBlock Margin="5">Sign in</TextBlock> 
            </StackPanel>
        </Button>
5. Hallo code codefragment toohello App.xaml.cs volgende toevoegen:

        protected override void OnActivated(IActivatedEventArgs args)
        {
            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                Frame content = Window.Current.Content as Frame;
                if (content.Content.GetType() == typeof(MainPage))
                {
                    content.Navigate(typeof(MainPage), protocolArgs.Uri);
                }
            }
            Window.Current.Activate();
            base.OnActivated(args);
        }
6. Package.appxmanifest bestand openen, te navigeren**declaraties**in **beschikbaar declaraties** vervolgkeuzelijst, selecteer **Protocol** en klik op **toevoegen** knop. Nu configureren Hallo **eigenschappen** Hallo **Protocol** declaratie. In **weergavenaam**, Hallo-naam die u wenst dat toodisplay toousers van uw toepassing toevoegen. In **naam**, uw {url_scheme_of_your_app} toevoegen.
7. Druk op Hallo F5 sleutel toorun Hallo app, klikt u op Hallo **aanmelden** knop en meld u aan bij Hallo-app met uw gekozen id-provider. Nadat de aanmeldingspagina geslaagd is, Hallo-app wordt uitgevoerd zonder fouten en u kunt tooquery zijn uw back-end en updates toodata maken.

## <a name="tokens"></a>Hallo-verificatietoken opslaan op Hallo-client
Hallo vorige voorbeeld hebt u geleerd een standaard aanmelden, waarvoor Hallo client toocontact beide Hallo id-provider en App Service Hallo telkens wanneer die Hallo-app wordt gestart. Is deze methode niet alleen inefficiënt, u kunt uitvoeren in gebruik-betrekking heeft problemen moeten probeert veel klanten toostart app op Hallo hetzelfde moment. Er is een betere benadering toocache Hallo verificatietoken geretourneerd door uw App Service en probeer toouse dit eerst voordat met behulp van een providergebaseerde aanmelden.

> [!NOTE]
> U kunt Hallo token dat is uitgegeven door App Services, ongeacht of u van verificatie van client beheerd of service gebruikmaakt-cache. Deze zelfstudie maakt gebruik van authentication service beheerd.
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a>Volgende stappen
Nu dat u deze basisverificatie-zelfstudie hebt voltooid, kunt u overwegen tooone Hallo volgende zelfstudies verder te gaan:

* [Push notifications tooyour app toevoegen](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Informatie over hoe tooyour app ondersteuning bieden voor pushmeldingen tooadd en pushmeldingen voor uw mobiele App back-end toouse Azure Notification Hubs toosend configureren.
* [Offlinesynchronisatie voor uw app inschakelen](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Meer informatie over hoe tooadd offline ondersteuning bieden voor uw app met een back-end voor de mobiele App. Offlinesynchronisatie kunnen eindgebruikers toointeract met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding.

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
