---
title: Verificatie toevoegen aan uw app Universal Windows Platform (UWP) | Microsoft Docs
description: 'Informatie over het gebruik van Azure App Service Mobile Apps voor verificatie van gebruikers van uw Universal Windows Platform (UWP)-app met een aantal identiteitsproviders, waaronder: AAD, Google, Facebook, Twitter en Microsoft.'
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
ms.openlocfilehash: 47da343d4ec956ec2e669757f56e853675f887a3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-windows-app"></a><span data-ttu-id="e85f9-103">Verificatie toevoegen aan uw Windows-app</span><span class="sxs-lookup"><span data-stu-id="e85f9-103">Add authentication to your Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="e85f9-104">Dit onderwerp leest u hoe u cloud-gebaseerde verificatie toevoegen aan uw mobiele app.</span><span class="sxs-lookup"><span data-stu-id="e85f9-104">This topic shows you how to add cloud-based authentication to your mobile app.</span></span> <span data-ttu-id="e85f9-105">In deze zelfstudie maakt toevoegen u verificatie aan de Universal Windows Platform (UWP)-Quick Start-project voor mobiele Apps met behulp van een id-provider die wordt ondersteund door Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="e85f9-105">In this tutorial, you add authentication to the Universal Windows Platform (UWP) quickstart project for Mobile Apps using an identity provider that is supported by Azure App Service.</span></span> <span data-ttu-id="e85f9-106">Na wordt is geverifieerd en gemachtigd door uw back-end voor de mobiele App, wordt de waarde van de gebruiker-ID weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e85f9-106">After being successfully authenticated and authorized by your Mobile App backend, the user ID value is displayed.</span></span>

<span data-ttu-id="e85f9-107">Deze zelfstudie is gebaseerd op de Snelstartgids Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="e85f9-107">This tutorial is based on the Mobile Apps quickstart.</span></span> <span data-ttu-id="e85f9-108">U moet eerst Voltooi de zelfstudie [aan de slag met Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e85f9-108">You must first complete the tutorial [Get started with Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).</span></span>

## <span data-ttu-id="e85f9-109"><a name="register"></a>Uw app registreren voor verificatie en de App Service configureren</span><span class="sxs-lookup"><span data-stu-id="e85f9-109"><a name="register"></a>Register your app for authentication and configure the App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="e85f9-110"><a name="redirecturl"></a>Uw app toevoegen aan de toegestane externe Omleidings-URL 's</span><span class="sxs-lookup"><span data-stu-id="e85f9-110"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="e85f9-111">Veilige verificatie vereist dat u een nieuwe URL-schema voor uw app definiëren.</span><span class="sxs-lookup"><span data-stu-id="e85f9-111">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="e85f9-112">Hierdoor kan de verificatiesysteem terug te keren naar uw app zodra het verificatieproces voltooid is.</span><span class="sxs-lookup"><span data-stu-id="e85f9-112">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="e85f9-113">In deze zelfstudie gebruiken we het URL-schema _appname_ in.</span><span class="sxs-lookup"><span data-stu-id="e85f9-113">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="e85f9-114">U kunt echter een URL-schema dat u kiest.</span><span class="sxs-lookup"><span data-stu-id="e85f9-114">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="e85f9-115">Deze moet uniek zijn voor uw mobiele App.</span><span class="sxs-lookup"><span data-stu-id="e85f9-115">It should be unique to your mobile application.</span></span> <span data-ttu-id="e85f9-116">De omleiding op de server inschakelen:</span><span class="sxs-lookup"><span data-stu-id="e85f9-116">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="e85f9-117">Selecteer in de [Azure-portal] uw App Service.</span><span class="sxs-lookup"><span data-stu-id="e85f9-117">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="e85f9-118">Klik op de **verificatie / autorisatie** menuoptie.</span><span class="sxs-lookup"><span data-stu-id="e85f9-118">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="e85f9-119">In de **toegestaan externe Omleidings-URL's**, voer `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="e85f9-119">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="e85f9-120">De **url_scheme_of_your_app** in deze tekenreeks wordt het URL-schema voor uw mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="e85f9-120">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="e85f9-121">Deze moet voldoen aan de normale URL-specificatie voor een protocol (Gebruik letters en cijfers alleen en begin met een letter).</span><span class="sxs-lookup"><span data-stu-id="e85f9-121">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="e85f9-122">U moet een notitie van de tekenreeks die u naar wens aanpassen van uw mobiele toepassingscode met het URL-schema op verschillende plaatsen.</span><span class="sxs-lookup"><span data-stu-id="e85f9-122">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="e85f9-123">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e85f9-123">Click **OK**.</span></span>

5. <span data-ttu-id="e85f9-124">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e85f9-124">Click **Save**.</span></span>

## <span data-ttu-id="e85f9-125"><a name="permissions"></a>Machtigingen beperken voor geverifieerde gebruikers</span><span class="sxs-lookup"><span data-stu-id="e85f9-125"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="e85f9-126">Nu kunt u controleren of anonieme toegang tot uw back-end is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e85f9-126">Now, you can verify that anonymous access to your backend has been disabled.</span></span> <span data-ttu-id="e85f9-127">Met de UWP-appproject ingesteld als het opstartproject, implementeren en uitvoeren van de app; Controleer of dat een niet-verwerkte uitzondering met een statuscode van 401 (niet-geautoriseerd) treedt op nadat de app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="e85f9-127">With the UWP app project set as the start-up project, deploy and run the app; verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="e85f9-128">Dit komt doordat de app probeert te krijgen tot uw mobiele App-Code als een niet-geverifieerde gebruiker, maar de *TodoItem* tabel nu is verificatie vereist.</span><span class="sxs-lookup"><span data-stu-id="e85f9-128">This happens because the app attempts to access your Mobile App Code as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="e85f9-129">Vervolgens kunt u de app om gebruikers te verifiëren voordat u resources van uw App Service wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e85f9-129">Next, you will update the app to authenticate users before requesting resources from your App Service.</span></span>

## <span data-ttu-id="e85f9-130"><a name="add-authentication"></a>Verificatie toevoegen aan de app.</span><span class="sxs-lookup"><span data-stu-id="e85f9-130"><a name="add-authentication"></a>Add authentication to the app</span></span>
1. <span data-ttu-id="e85f9-131">In de UWP app bestand MainPage.xaml.cs project en voeg het volgende codefragment toe:</span><span class="sxs-lookup"><span data-stu-id="e85f9-131">In the UWP app project file MainPage.xaml.cs and add the following code snippet:</span></span>
   
        // Define a member variable for storing the signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs the authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' to the name of your MobileServiceClient instance.
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
   
    <span data-ttu-id="e85f9-132">Deze code verifieert de gebruiker met een Facebook-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e85f9-132">This code authenticates the user with a Facebook login.</span></span> <span data-ttu-id="e85f9-133">Als u van een id-provider dan Facebook gebruikmaakt, wijzigt u de waarde van **MobileServiceAuthenticationProvider** boven aan de waarde voor de provider.</span><span class="sxs-lookup"><span data-stu-id="e85f9-133">If you are using an identity provider other than Facebook, change the value of **MobileServiceAuthenticationProvider** above to the value for your provider.</span></span>
2. <span data-ttu-id="e85f9-134">Vervang de **OnNavigatedTo()** methode in MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="e85f9-134">Replace the **OnNavigatedTo()** method in MainPage.xaml.cs.</span></span> <span data-ttu-id="e85f9-135">Vervolgens voegt u een **aanmelden** knop naar de app waarmee de verificatie wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="e85f9-135">Next, you will add a **Sign in** button to the app that triggers authentication.</span></span>

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. <span data-ttu-id="e85f9-136">Het volgende codefragment aan MainPage.xaml.cs toevoegen:</span><span class="sxs-lookup"><span data-stu-id="e85f9-136">Add the following code snippet to the MainPage.xaml.cs:</span></span>
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login the user and then load data from the mobile app.
            if (await AuthenticateAsync())
            {
                // Switch the buttons and load items from the mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. <span data-ttu-id="e85f9-137">Open het projectbestand MainPage.xaml, zoek het element dat definieert de **opslaan** knop en vervang deze door de volgende code:</span><span class="sxs-lookup"><span data-stu-id="e85f9-137">Open the MainPage.xaml project file, locate the element that defines the **Save** button and replace it with the following code:</span></span>
   
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
5. <span data-ttu-id="e85f9-138">Het volgende codefragment toevoegen aan de App.xaml.cs:</span><span class="sxs-lookup"><span data-stu-id="e85f9-138">Add the following code snippet to the App.xaml.cs:</span></span>

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
6. <span data-ttu-id="e85f9-139">Package.appxmanifest bestand openen, gaat u naar **declaraties**in **beschikbaar declaraties** vervolgkeuzelijst, selecteer **Protocol** en klik op **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="e85f9-139">Open Package.appxmanifest file, navigate to **Declarations**, in **Available Declarations** dropdown list, select **Protocol** and click **Add** button.</span></span> <span data-ttu-id="e85f9-140">Nu configureren de **eigenschappen** van de **Protocol** declaratie.</span><span class="sxs-lookup"><span data-stu-id="e85f9-140">Now configure the **Properties** of the **Protocol** declaration.</span></span> <span data-ttu-id="e85f9-141">In **weergavenaam**, de naam die u wilt weergeven aan gebruikers van uw toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e85f9-141">In **Display name**, add the name you wish to display to users of your application.</span></span> <span data-ttu-id="e85f9-142">In **naam**, uw {url_scheme_of_your_app} toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e85f9-142">In **Name**, add your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="e85f9-143">Druk op F5 bij het uitvoeren van de app en klik op de **aanmelden** knop en meld u aan bij de app met uw gekozen id-provider.</span><span class="sxs-lookup"><span data-stu-id="e85f9-143">Press the F5 key to run the app, click the **Sign in** button, and sign into the app with your chosen identity provider.</span></span> <span data-ttu-id="e85f9-144">Nadat de aanmeldingspagina geslaagd is, de app wordt uitgevoerd zonder fouten en kunt u uw back-end doorzoeken en updates aanbrengen in de gegevens.</span><span class="sxs-lookup"><span data-stu-id="e85f9-144">After your sign-in is successful, the app runs without errors and you are able to query your backend and make updates to data.</span></span>

## <span data-ttu-id="e85f9-145"><a name="tokens"></a>Het verificatietoken opslaan op de client</span><span class="sxs-lookup"><span data-stu-id="e85f9-145"><a name="tokens"></a>Store the authentication token on the client</span></span>
<span data-ttu-id="e85f9-146">Het vorige voorbeeld blijkt een standaard aanmelden, die vereist dat de client te maken met zowel de id-provider en de App Service elke keer dat de app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="e85f9-146">The previous example showed a standard sign-in, which requires the client to contact both the identity provider and the App Service every time that the app starts.</span></span> <span data-ttu-id="e85f9-147">Is deze methode niet alleen inefficiënt, u kunt uitvoeren in gebruik-betrekking heeft problemen moeten veel klanten proberen app starten op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="e85f9-147">Not only is this method inefficient, you can run into usage-relates issues should many customers try to start you app at the same time.</span></span> <span data-ttu-id="e85f9-148">Er is een betere benadering voor het verificatietoken dat wordt geretourneerd door de Service van uw App in de cache en probeer het eerst moet worden gebruikt deze voordat u een provider gebaseerde aanmelden.</span><span class="sxs-lookup"><span data-stu-id="e85f9-148">A better approach is to cache the authorization token returned by your App Service and try to use this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="e85f9-149">U kunt het token dat is uitgegeven door App Services, ongeacht of u van verificatie van client beheerd of service gebruikmaakt-cache.</span><span class="sxs-lookup"><span data-stu-id="e85f9-149">You can cache the token issued by App Services regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="e85f9-150">Deze zelfstudie maakt gebruik van authentication service beheerd.</span><span class="sxs-lookup"><span data-stu-id="e85f9-150">This tutorial uses service-managed authentication.</span></span>
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="e85f9-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e85f9-151">Next steps</span></span>
<span data-ttu-id="e85f9-152">Nu dat u deze basisverificatie-zelfstudie hebt voltooid, overweeg dan u verder gaat u aan bij een van de volgende zelfstudies:</span><span class="sxs-lookup"><span data-stu-id="e85f9-152">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="e85f9-153">Pushmeldingen toevoegen aan uw app</span><span class="sxs-lookup"><span data-stu-id="e85f9-153">Add push notifications to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="e85f9-154">Informatie over het toevoegen van ondersteuning van pushmeldingen aan uw app en het configureren van de backend voor mobiele apps voor gebruik van Azure Notification Hubs voor het verzenden van pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="e85f9-154">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="e85f9-155">Offlinesynchronisatie voor uw app inschakelen</span><span class="sxs-lookup"><span data-stu-id="e85f9-155">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="e85f9-156">Informatie over het toevoegen van offlineondersteuning aan uw app met een back-end voor mobiele apps.</span><span class="sxs-lookup"><span data-stu-id="e85f9-156">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="e85f9-157">Met offlinesynchronisatie kunnen eindgebruikers interactie aangaan met een mobiele app&mdash;gegevens weergeven, toevoegen of wijzigen&mdash;ook als er geen netwerkverbinding is.</span><span class="sxs-lookup"><span data-stu-id="e85f9-157">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
