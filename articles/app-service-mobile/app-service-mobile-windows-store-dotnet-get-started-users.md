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
# <a name="add-authentication-tooyour-windows-app"></a><span data-ttu-id="2a373-103">Verificatie tooyour Windows-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="2a373-103">Add authentication tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="2a373-104">Dit onderwerp leest u hoe tooadd cloudverificatie tooyour mobiele app.</span><span class="sxs-lookup"><span data-stu-id="2a373-104">This topic shows you how tooadd cloud-based authentication tooyour mobile app.</span></span> <span data-ttu-id="2a373-105">In deze zelfstudie kunt u verificatie toohello Universal Windows Platform (UWP)-Quick Start-project toevoegen voor mobiele Apps met behulp van een id-provider die wordt ondersteund door Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="2a373-105">In this tutorial, you add authentication toohello Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="2a373-106">Na wordt is geverifieerd en gemachtigd door uw back-end voor de mobiele App, wordt Hallo gebruiker-ID-waarde weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2a373-106">After being successfully authenticated and authorized by your Mobile App backend, hello user ID value is displayed.</span></span>

<span data-ttu-id="2a373-107">Deze zelfstudie is gebaseerd op Hallo Mobile Apps-Quick Start.</span><span class="sxs-lookup"><span data-stu-id="2a373-107">This tutorial is based on hello Mobile Apps quickstart.</span></span> <span data-ttu-id="2a373-108">U moet eerst Hallo-zelfstudie hebt voltooid [aan de slag met Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2a373-108">You must first complete hello tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="2a373-109"><a name="register"></a>Uw app registreren voor verificatie en Hallo App Service configureren</span><span class="sxs-lookup"><span data-stu-id="2a373-109"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="2a373-110"><a name="redirecturl"></a>Uw app toohello toegestane externe Omleidings-URL's toevoegen</span><span class="sxs-lookup"><span data-stu-id="2a373-110"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="2a373-111">Veilige verificatie vereist dat u een nieuwe URL-schema voor uw app definiëren.</span><span class="sxs-lookup"><span data-stu-id="2a373-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="2a373-112">Hierdoor Hallo verificatie system tooredirect back tooyour app zodra de Hallo verificatieproces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="2a373-112">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="2a373-113">In deze zelfstudie gebruiken we Hallo URL-schema _appname_ in.</span><span class="sxs-lookup"><span data-stu-id="2a373-113">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="2a373-114">U kunt echter een URL-schema dat u kiest.</span><span class="sxs-lookup"><span data-stu-id="2a373-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="2a373-115">Deze moet uniek tooyour mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="2a373-115">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="2a373-116">Hallo-omleiding tooenable aan serverzijde Hallo:</span><span class="sxs-lookup"><span data-stu-id="2a373-116">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="2a373-117">Selecteer in de Hallo [Azure portal], uw App Service.</span><span class="sxs-lookup"><span data-stu-id="2a373-117">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="2a373-118">Klik op Hallo **verificatie / autorisatie** menuoptie.</span><span class="sxs-lookup"><span data-stu-id="2a373-118">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="2a373-119">In Hallo **toegestaan externe Omleidings-URL's**, voer `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="2a373-119">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="2a373-120">Hallo **url_scheme_of_your_app** in deze reeks is Hallo URL-schema voor uw mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="2a373-120">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="2a373-121">Deze moet voldoen aan de normale URL-specificatie voor een protocol (Gebruik letters en cijfers alleen en begin met een letter).</span><span class="sxs-lookup"><span data-stu-id="2a373-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="2a373-122">U moet een notitie van Hallo-tekenreeks die u kiest, want u tooadjust uw code mobiele toepassing Hello URL-schema op verschillende plaatsen moet.</span><span class="sxs-lookup"><span data-stu-id="2a373-122">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="2a373-123">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2a373-123">Click **OK**.</span></span>

5. <span data-ttu-id="2a373-124">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2a373-124">Click **Save**.</span></span>

## <span data-ttu-id="2a373-125"><a name="permissions"></a>Machtigingen tooauthenticated gebruikers beperken</span><span class="sxs-lookup"><span data-stu-id="2a373-125"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="2a373-126">U kunt nu controleren dat die back-end voor anonieme toegang tooyour is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2a373-126">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="2a373-127">Met de Hallo UWP-appproject instellen als opstartproject hello, implementeren en uitvoeren van Hallo app; Controleer of dat een niet-verwerkte uitzondering met een statuscode van 401 (niet-geautoriseerd) treedt op nadat het Hallo-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2a373-127">With hello UWP app project set as hello start-up project, deploy and run hello app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="2a373-128">Dit gebeurt omdat Hallo app probeert tooaccess op uw mobiele App-Code als een niet-geverifieerde gebruiker, maar Hallo *TodoItem* tabel nu is verificatie vereist.</span><span class="sxs-lookup"><span data-stu-id="2a373-128">This happens because hello app attempts tooaccess your Mobile App Code as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="2a373-129">Vervolgens wordt u Hallo app tooauthenticate gebruikers bijwerken voordat u resources van uw App Service.</span><span class="sxs-lookup"><span data-stu-id="2a373-129">Next, you will update hello app tooauthenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="2a373-130"><a name="add-authentication"></a>Verificatie toohello app toevoegen</span><span class="sxs-lookup"><span data-stu-id="2a373-130"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="2a373-131">In de UWP-appproject Hallo bestand MainPage.xaml.cs en Hallo codefragment volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2a373-131">In hello UWP app project file MainPage.xaml.cs and add hello following code snippet:</span></span>
   
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
   
    <span data-ttu-id="2a373-132">Deze code verifieert Hallo-gebruiker met een Facebook-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="2a373-132">This code authenticates hello user with a Facebook login.</span></span> <span data-ttu-id="2a373-133">Als u van een id-provider dan Facebook gebruikmaakt, wijzigt u de waarde Hallo van **MobileServiceAuthenticationProvider** boven toohello waarde voor de provider.</span><span class="sxs-lookup"><span data-stu-id="2a373-133">If you are using an identity provider other than Facebook, change hello value of **MobileServiceAuthenticationProvider** above toohello value for your provider.</span></span>
2. <span data-ttu-id="2a373-134">Vervang Hallo **OnNavigatedTo()** methode in MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="2a373-134">Replace hello **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="2a373-135">Vervolgens voegt u een **aanmelden** knop toohello app waarmee de verificatie wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="2a373-135">Next, you will add a **Sign in** button toohello app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="2a373-136">Hallo code codefragment toohello MainPage.xaml.cs volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2a373-136">Add hello following code snippet toohello MainPage.xaml.cs:</span></span>
   
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
4. <span data-ttu-id="2a373-137">Hallo MainPage.xaml projectbestand openen, zoek naar Hallo-element waarmee wordt gedefinieerd Hallo **opslaan** knop en vervang deze door Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="2a373-137">Open hello MainPage.xaml project file, locate hello element that defines hello **Save** button and replace it with hello following code:</span></span>
   
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
5. <span data-ttu-id="2a373-138">Hallo code codefragment toohello App.xaml.cs volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="2a373-138">Add hello following code snippet toohello App.xaml.cs:</span></span>

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
6. <span data-ttu-id="2a373-139">Package.appxmanifest bestand openen, te navigeren**declaraties**in **beschikbaar declaraties** vervolgkeuzelijst, selecteer **Protocol** en klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="2a373-139">Open Package.appxmanifest file, navigate too**Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="2a373-140">Nu configureren Hallo **eigenschappen** Hallo **Protocol** declaratie.</span><span class="sxs-lookup"><span data-stu-id="2a373-140">Now configure hello **Properties** of hello **Protocol** declaration.</span></span> <span data-ttu-id="2a373-141">In **weergavenaam**, Hallo-naam die u wenst dat toodisplay toousers van uw toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2a373-141">In **Display name**, add hello name you wish toodisplay toousers of your application.</span></span> <span data-ttu-id="2a373-142">In **naam**, uw {url_scheme_of_your_app} toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2a373-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="2a373-143">Druk op Hallo F5 sleutel toorun Hallo app, klikt u op Hallo **aanmelden** knop en meld u aan bij Hallo-app met uw gekozen id-provider.</span><span class="sxs-lookup"><span data-stu-id="2a373-143">Press hello F5 key toorun hello app, click hello **Sign in** button, and sign into hello app with your chosen identity provider.</span></span> <span data-ttu-id="2a373-144">Nadat de aanmeldingspagina geslaagd is, Hallo-app wordt uitgevoerd zonder fouten en u kunt tooquery zijn uw back-end en updates toodata maken.</span><span class="sxs-lookup"><span data-stu-id="2a373-144">After your sign-in is successful, hello app runs without errors and you are able tooquery your backend and make updates toodata.</span></span>

## <span data-ttu-id="2a373-145"><a name="tokens"></a>Hallo-verificatietoken opslaan op Hallo-client</span><span class="sxs-lookup"><span data-stu-id="2a373-145"><a name="tokens"></a>Store hello authentication token on hello client</span></span>
<span data-ttu-id="2a373-146">Hallo vorige voorbeeld hebt u geleerd een standaard aanmelden, waarvoor Hallo client toocontact beide Hallo id-provider en App Service Hallo telkens wanneer die Hallo-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2a373-146">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello App Service every time that hello app starts.</span></span> <span data-ttu-id="2a373-147">Is deze methode niet alleen inefficiënt, u kunt uitvoeren in gebruik-betrekking heeft problemen moeten probeert veel klanten toostart app op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="2a373-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try toostart you app at hello same time.</span></span> <span data-ttu-id="2a373-148">Er is een betere benadering toocache Hallo verificatietoken geretourneerd door uw App Service en probeer toouse dit eerst voordat met behulp van een providergebaseerde aanmelden.</span><span class="sxs-lookup"><span data-stu-id="2a373-148">A better approach is toocache hello authorization token returned by your App Service and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="2a373-149">U kunt Hallo token dat is uitgegeven door App Services, ongeacht of u van verificatie van client beheerd of service gebruikmaakt-cache.</span><span class="sxs-lookup"><span data-stu-id="2a373-149">You can cache hello token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="2a373-150">Deze zelfstudie maakt gebruik van authentication service beheerd.</span><span class="sxs-lookup"><span data-stu-id="2a373-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="2a373-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2a373-151">Next steps</span></span>
<span data-ttu-id="2a373-152">Nu dat u deze basisverificatie-zelfstudie hebt voltooid, kunt u overwegen tooone Hallo volgende zelfstudies verder te gaan:</span><span class="sxs-lookup"><span data-stu-id="2a373-152">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="2a373-153">Push notifications tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="2a373-153">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="2a373-154">Informatie over hoe tooyour app ondersteuning bieden voor pushmeldingen tooadd en pushmeldingen voor uw mobiele App back-end toouse Azure Notification Hubs toosend configureren.</span><span class="sxs-lookup"><span data-stu-id="2a373-154">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="2a373-155">Offlinesynchronisatie voor uw app inschakelen</span><span class="sxs-lookup"><span data-stu-id="2a373-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="2a373-156">Meer informatie over hoe tooadd offline ondersteuning bieden voor uw app met een back-end voor de mobiele App.</span><span class="sxs-lookup"><span data-stu-id="2a373-156">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="2a373-157">Offlinesynchronisatie kunnen eindgebruikers toointeract met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="2a373-157">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
