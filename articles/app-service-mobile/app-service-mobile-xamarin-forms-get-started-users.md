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
# <a name="add-authentication-tooyour-xamarin-forms-app"></a><span data-ttu-id="7ce4a-103">Verificatie tooyour Xamarin Forms app toevoegen</span><span class="sxs-lookup"><span data-stu-id="7ce4a-103">Add authentication tooyour Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="7ce4a-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="7ce4a-104">Overview</span></span>
<span data-ttu-id="7ce4a-105">Dit onderwerp leest u hoe tooauthenticate gebruikers van een App Service Mobile App van uw clienttoepassing.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-105">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="7ce4a-106">In deze zelfstudie kunt u verificatie toevoegen aan Hallo Xamarin Forms Quick Start-project met behulp van een id-provider die wordt ondersteund door App Service.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-106">In this tutorial, you add authentication to hello Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="7ce4a-107">Nadat wordt is geverifieerd en geautoriseerd door uw mobiele App, Hallo gebruiker-id-waarde wordt weergegeven en kunt u zich tabelgegevens kunnen tooaccess beperkt.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-107">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed, and you will be able tooaccess restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ce4a-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7ce4a-108">Prerequisites</span></span>
<span data-ttu-id="7ce4a-109">Voor Hallo beste resultaat in deze zelfstudie, raden we u eerst Hallo voltooid [maken van een app voor Xamarin Forms] [ 1] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-109">For hello best result with this tutorial, we recommend that you first complete hello [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="7ce4a-110">Nadat u deze zelfstudie hebt voltooid, hebt u een Xamarin Forms-project dat een TodoList-App voor meerdere platforms.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="7ce4a-111">Als u geen gebruik Hallo snel starten-serverproject gedownload, moet u Hallo verificatie pakket tooyour extensieproject toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-111">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="7ce4a-112">Zie voor meer informatie over server extensiepakketten [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="7ce4a-112">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="7ce4a-113">Uw app registreren voor verificatie en App-Services configureren</span><span class="sxs-lookup"><span data-stu-id="7ce4a-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="7ce4a-114"><a name="redirecturl"></a>Uw app toohello toegestane externe Omleidings-URL's toevoegen</span><span class="sxs-lookup"><span data-stu-id="7ce4a-114"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="7ce4a-115">Veilige verificatie vereist dat u een nieuwe URL-schema voor uw app definiëren.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="7ce4a-116">Hierdoor Hallo verificatie system tooredirect back tooyour app zodra de Hallo verificatieproces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-116">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="7ce4a-117">In deze zelfstudie gebruiken we Hallo URL-schema _appname_ in.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-117">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="7ce4a-118">U kunt echter een URL-schema dat u kiest.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="7ce4a-119">Deze moet uniek tooyour mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-119">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="7ce4a-120">Hallo-omleiding tooenable aan serverzijde Hallo:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-120">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="7ce4a-121">Selecteer in de Hallo [Azure portal], uw App Service.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-121">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="7ce4a-122">Klik op Hallo **verificatie / autorisatie** menuoptie.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-122">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="7ce4a-123">In Hallo **toegestaan externe Omleidings-URL's**, voer `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-123">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="7ce4a-124">Hallo **url_scheme_of_your_app** in deze reeks is Hallo URL-schema voor uw mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-124">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="7ce4a-125">Deze moet voldoen aan de normale URL-specificatie voor een protocol (Gebruik letters en cijfers alleen en begin met een letter).</span><span class="sxs-lookup"><span data-stu-id="7ce4a-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="7ce4a-126">U moet een notitie van Hallo-tekenreeks die u kiest, want u tooadjust uw code mobiele toepassing Hello URL-schema op verschillende plaatsen moet.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-126">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="7ce4a-127">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-127">Click **OK**.</span></span>

5. <span data-ttu-id="7ce4a-128">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-128">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="7ce4a-129">Machtigingen tooauthenticated gebruikers beperken</span><span class="sxs-lookup"><span data-stu-id="7ce4a-129">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a><span data-ttu-id="7ce4a-130">Verificatie toohello draagbare klassebibliotheek toevoegen</span><span class="sxs-lookup"><span data-stu-id="7ce4a-130">Add authentication toohello portable class library</span></span>
<span data-ttu-id="7ce4a-131">Hallo maakt gebruik van Mobile Apps [LoginAsync] [ 3] uitbreidingsmethode op Hallo [MobileServiceClient] [ 4] toosign in een gebruiker met App Service -verificatie.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-131">Mobile Apps uses hello [LoginAsync][3] extension method on hello [MobileServiceClient][4] toosign in a user with App Service authentication.</span></span> <span data-ttu-id="7ce4a-132">Dit voorbeeld wordt een beheerde server authenticatiestroom die wordt weergegeven van de provider Hallo aanmelden interface in Hallo app gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-132">This sample uses a server-managed authentication flow that displays hello provider's sign-in interface in hello app.</span></span> <span data-ttu-id="7ce4a-133">Zie voor meer informatie [authentication Server beheerd][5].</span><span class="sxs-lookup"><span data-stu-id="7ce4a-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="7ce4a-134">Voor een betere gebruikerservaring in uw productie-app, moet u rekening houden met gebruik van [Client beheerd verificatie][6].</span><span class="sxs-lookup"><span data-stu-id="7ce4a-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="7ce4a-135">tooauthenticate aan een project Xamarin Forms definiëren een **IAuthenticate** Hallo Portable Class Library voor Hallo app-interface.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-135">tooauthenticate with a Xamarin Forms project, define an **IAuthenticate** interface in hello Portable Class Library for hello app.</span></span> <span data-ttu-id="7ce4a-136">Voeg vervolgens een **aanmelden** knop toohello-gebruikersinterface is gedefinieerd in Hallo draagbare klassebibliotheek, die u op toostart verificatie.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-136">Then add a **Sign-in** button toohello user interface defined in hello Portable Class Library, which you click toostart authentication.</span></span> <span data-ttu-id="7ce4a-137">Gegevens worden geladen vanuit Hallo mobiele app back-end na een geslaagde authenticatie.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-137">Data is loaded from hello mobile app backend after successful authentication.</span></span>

<span data-ttu-id="7ce4a-138">Implementeer Hallo **IAuthenticate** interface voor elk platform dat wordt ondersteund door uw app.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-138">Implement hello **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="7ce4a-139">Open in Visual Studio of Xamarin Studio App.cs van Hallo-project met **draagbare** in naam van Hallo Portable Class Library-project is, voegt u Hallo volgende `using` instructie:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-139">In Visual Studio or Xamarin Studio, open App.cs from hello project with **Portable** in hello name, which is Portable Class Library project, then  add hello following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="7ce4a-140">Voeg de volgende Hallo in App.cs, `IAuthenticate` interface definition direct vóór de Hallo `App` definitie van klasse.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-140">In App.cs, add hello following `IAuthenticate` interface definition immediately before hello `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="7ce4a-141">tooinitialize hello interface met een implementatie platform-specifieke toevoegen na de statische leden toohello Hallo **App** klasse.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-141">tooinitialize hello interface with a platform-specific implementation, add hello following static members toohello **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="7ce4a-142">TodoList.xaml openen vanuit Hallo Portable Class Library-project, voeg de volgende Hallo **knop** -element in Hallo *buttonsPanel* lay-element na Hallo bestaande knop:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-142">Open TodoList.xaml from hello Portable Class Library project, add hello following **Button** element in hello *buttonsPanel* layout element, after hello existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="7ce4a-143">Deze knop activeert verificatie met uw mobiele app back-end server beheerd.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="7ce4a-144">TodoList.xaml.cs openen vanuit Hallo Portable Class Library-project, voeg dan Hallo volgende veld toohello `TodoList` klasse:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-144">Open TodoList.xaml.cs from hello Portable Class Library project, then add hello following field toohello `TodoList` class:</span></span>

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="7ce4a-145">Vervang Hallo **OnAppearing** methode Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-145">Replace hello **OnAppearing** method with hello following code:</span></span>

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

    <span data-ttu-id="7ce4a-146">Deze code zorgt ervoor dat de gegevens alleen vernieuwd van Hallo-service nadat u hebt geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-146">This code makes sure that data is only refreshed from hello service after you have been authenticated.</span></span>
7. <span data-ttu-id="7ce4a-147">Hallo-handler voor Hallo na toevoegen **op wordt geklikt** gebeurtenis toohello **TodoList** klasse:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-147">Add hello following handler for hello **Clicked** event toohello **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="7ce4a-148">De wijzigingen opslaan en opnieuw opbouwen Hallo Portable Class Library project zonder fouten te controleren.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-148">Save your changes and rebuild hello Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-toohello-android-app"></a><span data-ttu-id="7ce4a-149">Verificatie toohello Android-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="7ce4a-149">Add authentication toohello Android app</span></span>
<span data-ttu-id="7ce4a-150">Deze sectie wordt beschreven hoe tooimplement hello **IAuthenticate** interface in Hallo Android-app-project.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-150">This section shows how tooimplement hello **IAuthenticate** interface in hello Android app project.</span></span> <span data-ttu-id="7ce4a-151">Deze sectie overslaan als Android-apparaten worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="7ce4a-152">In Visual Studio of Xamarin Studio, met de rechtermuisknop op Hallo **droid** project, klikt u vervolgens **instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-152">In Visual Studio or Xamarin Studio, right-click hello **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="7ce4a-153">Druk op F5 toostart Hallo project in Hallo foutopsporingsprogramma en controleer of dat een niet-verwerkte uitzondering met een statuscode van 401 (niet-geautoriseerd) treedt op nadat de app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-153">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="7ce4a-154">Hallo 401 code wordt geproduceerd omdat beperkte tooauthorized gebruikers alleen toegang op Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-154">hello 401 code is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="7ce4a-155">MainActivity.cs opent in Hallo Android-project en voeg de volgende Hallo `using` instructies:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-155">Open MainActivity.cs in hello Android project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="7ce4a-156">Update Hallo **MainActivity** klasse tooimplement hello **IAuthenticate** interface, als volgt:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-156">Update hello **MainActivity** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="7ce4a-157">Update Hallo **MainActivity** klasse door toe te voegen een **MobileServiceUser** veld en een **verifiëren** methode die wordt door Hallo vereist **IAuthenticate**  interface, als volgt:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-157">Update hello **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

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

    <span data-ttu-id="7ce4a-158">Als u van een id-provider dan Facebook gebruikmaakt, kiest u een andere waarde voor [MobileServiceAuthenticationProvider][7].</span><span class="sxs-lookup"><span data-stu-id="7ce4a-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="7ce4a-159">Hallo-code in volgende toevoegen <application> knooppunt van AndroidManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-159">Add hello following code inside <application> node of AndroidManifest.xml:</span></span>

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

1. <span data-ttu-id="7ce4a-160">Hallo na code toohello toevoegen **OnCreate** methode Hallo **MainActivity** klasse vóór Hallo aanroep te`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-160">Add hello following code toohello **OnCreate** method of hello **MainActivity** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="7ce4a-161">Deze code wordt ervoor gezorgd Hallo verificator wordt geïnitialiseerd voordat Hallo app geladen.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-161">This code ensures hello authenticator is initialized before hello app loads.</span></span>
2. <span data-ttu-id="7ce4a-162">Hallo app opnieuw samenstellen, uitvoeren en meld u aan met de Hallo verificatieprovider u hebt gekozen en controleer of dat u kunt tooaccess gegevens als een geverifieerde gebruiker zijn.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-162">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toohello-ios-app"></a><span data-ttu-id="7ce4a-163">Verificatie toohello iOS-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="7ce4a-163">Add authentication toohello iOS app</span></span>
<span data-ttu-id="7ce4a-164">Deze sectie wordt beschreven hoe tooimplement hello **IAuthenticate** interface in Hallo iOS-app-project.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-164">This section shows how tooimplement hello **IAuthenticate** interface in hello iOS app project.</span></span> <span data-ttu-id="7ce4a-165">Deze sectie overslaan als iOS-apparaten worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-165">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="7ce4a-166">In Visual Studio of Xamarin Studio, met de rechtermuisknop op Hallo **iOS** project, klikt u vervolgens **instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-166">In Visual Studio or Xamarin Studio, right-click hello **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="7ce4a-167">Druk op F5 toostart Hallo project in Hallo foutopsporingsprogramma en controleer of dat een niet-verwerkte uitzondering met een statuscode van 401 (niet-geautoriseerd) treedt op nadat het Hallo-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-167">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="7ce4a-168">Hallo 401-respons wordt geproduceerd omdat beperkte tooauthorized gebruikers alleen toegang op Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-168">hello 401 response is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="7ce4a-169">AppDelegate.cs opent in Hallo iOS-project en voeg de volgende Hallo `using` instructies:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-169">Open AppDelegate.cs in hello iOS project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="7ce4a-170">Update Hallo **AppDelegate** klasse tooimplement hello **IAuthenticate** interface, als volgt:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-170">Update hello **AppDelegate** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="7ce4a-171">Update Hallo **AppDelegate** klasse door toe te voegen een **MobileServiceUser** veld en een **verifiëren** methode die wordt door Hallo vereist **IAuthenticate**  interface, als volgt:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-171">Update hello **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

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

    <span data-ttu-id="7ce4a-172">Als u van een id-provider dan Facebook gebruikmaakt, kiest u een andere waarde voor [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="7ce4a-172">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

6. <span data-ttu-id="7ce4a-173">Hallo AppDelegate klasse bijwerken door toe te voegen methode-overload OpenUrl (UIApplication NSUrl-url-app NSDictionary opties)</span><span class="sxs-lookup"><span data-stu-id="7ce4a-173">Update hello AppDelegate class by adding OpenUrl(UIApplication app, NSUrl url, NSDictionary options) method overload</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. <span data-ttu-id="7ce4a-174">Toevoegen van de volgende regel code toohello hello **FinishedLaunching** te aanroep van servermethode voordat Hallo`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-174">Add hello following line of code toohello **FinishedLaunching** method before hello call too`LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="7ce4a-175">Deze code wordt ervoor gezorgd Hallo verificator is geïnitialiseerd voordat de app hello wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-175">This code ensures hello authenticator is initialized before hello app is loaded.</span></span>

6. <span data-ttu-id="7ce4a-176">Voeg **{url_scheme_of_your_app}** tooURL-schema's in de Info.plist.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-176">Add **{url_scheme_of_your_app}** tooURL Schemes in Info.plist.</span></span>

7. <span data-ttu-id="7ce4a-177">Hallo app opnieuw samenstellen, uitvoeren en meld u aan met de Hallo verificatieprovider u hebt gekozen en controleer of dat u kunt tooaccess gegevens als een geverifieerde gebruiker zijn.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-177">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a><span data-ttu-id="7ce4a-178">Toevoegen van verificatie tooWindows 10 (inclusief Phone) app-projecten</span><span class="sxs-lookup"><span data-stu-id="7ce4a-178">Add authentication tooWindows 10 (including Phone) app projects</span></span>
<span data-ttu-id="7ce4a-179">Deze sectie wordt beschreven hoe tooimplement hello **IAuthenticate** interface in Hallo Windows 10-app-projecten.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-179">This section shows how tooimplement hello **IAuthenticate** interface in hello Windows 10 app projects.</span></span> <span data-ttu-id="7ce4a-180">Hallo dezelfde stappen van toepassing op Universal Windows Platform (UWP)-projecten, maar het gebruik van Hallo **UWP** project (met vermelde wijzigingen).</span><span class="sxs-lookup"><span data-stu-id="7ce4a-180">hello same steps apply for Universal Windows Platform (UWP) projects, but using hello **UWP** project (with noted changes).</span></span> <span data-ttu-id="7ce4a-181">Deze sectie overslaan als Windows-apparaten worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-181">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="7ce4a-182">' In Visual Studio met de rechtermuisknop op beide Hallo **UWP** project, klikt u vervolgens **instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-182">"In Visual Studio, right-click either hello **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="7ce4a-183">Druk op F5 toostart Hallo project in Hallo foutopsporingsprogramma en controleer of dat een niet-verwerkte uitzondering met een statuscode van 401 (niet-geautoriseerd) treedt op nadat het Hallo-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-183">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="7ce4a-184">Hallo 401-respons gebeurt omdat beperkte tooauthorized gebruikers alleen toegang op Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-184">hello 401 response happens because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="7ce4a-185">MainPage.xaml.cs open voor Hallo Windows app-project en voeg de volgende Hallo `using` instructies:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-185">Open MainPage.xaml.cs for hello Windows app project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="7ce4a-186">Vervang `<your_Portable_Class_Library_namespace>` met Hallo naamruimte voor uw draagbare klassebibliotheek.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-186">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>
4. <span data-ttu-id="7ce4a-187">Update Hallo **MainPage** klasse tooimplement hello **IAuthenticate** interface, als volgt:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-187">Update hello **MainPage** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="7ce4a-188">Update Hallo **MainPage** klasse door toe te voegen een **MobileServiceUser** veld en een **verifiëren** methode die wordt door Hallo vereist **IAuthenticate** interface, als volgt:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-188">Update hello **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

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

    <span data-ttu-id="7ce4a-189">Als u van een id-provider dan Facebook gebruikmaakt, kiest u een andere waarde voor [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="7ce4a-189">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="7ce4a-190">Toevoegen van de volgende coderegel in de constructor voor Hallo HALLO hallo **MainPage** klasse vóór Hallo aanroep te`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-190">Add hello following line of code in hello constructor for hello **MainPage** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="7ce4a-191">Vervang `<your_Portable_Class_Library_namespace>` met Hallo naamruimte voor uw draagbare klassebibliotheek.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-191">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>

3. <span data-ttu-id="7ce4a-192">Als u **UWP**, voeg de volgende Hallo **OnActivated** methode overschrijven toohello **App** klasse:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-192">If you are using **UWP**, add hello following **OnActivated** method override toohello **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   <span data-ttu-id="7ce4a-193">Hallo methode overschrijven wanneer al bestaat, voorwaardelijke code Hallo van Hallo voorgaande codefragment toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-193">When hello method override already exists, add hello conditional code from hello preceding snippet.</span></span>  <span data-ttu-id="7ce4a-194">Deze code is niet vereist voor universele Windows-projecten.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-194">This code is not required for Universal Windows projects.</span></span>

3. <span data-ttu-id="7ce4a-195">Voeg **{url_scheme_of_your_app}** in Package.appxmanifest.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-195">Add **{url_scheme_of_your_app}** in Package.appxmanifest.</span></span> 

4. <span data-ttu-id="7ce4a-196">Hallo app opnieuw samenstellen, uitvoeren en meld u aan met de Hallo verificatieprovider u hebt gekozen en controleer of dat u kunt tooaccess gegevens als een geverifieerde gebruiker zijn.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-196">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ce4a-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7ce4a-197">Next steps</span></span>
<span data-ttu-id="7ce4a-198">Nu dat u deze basisverificatie-zelfstudie hebt voltooid, kunt u overwegen tooone Hallo volgende zelfstudies verder te gaan:</span><span class="sxs-lookup"><span data-stu-id="7ce4a-198">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="7ce4a-199">Push notifications tooyour app toevoegen</span><span class="sxs-lookup"><span data-stu-id="7ce4a-199">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="7ce4a-200">Informatie over hoe tooyour app ondersteuning bieden voor pushmeldingen tooadd en pushmeldingen voor uw mobiele App back-end toouse Azure Notification Hubs toosend configureren.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-200">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="7ce4a-201">Offlinesynchronisatie voor uw app inschakelen</span><span class="sxs-lookup"><span data-stu-id="7ce4a-201">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="7ce4a-202">Meer informatie over hoe tooadd offline ondersteuning bieden voor uw app met een back-end voor de mobiele App.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-202">Learn how tooadd offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="7ce4a-203">Offlinesynchronisatie kunnen eindgebruikers gebruikers toointeract met een mobiele app - weergeven, toevoegen of wijzigen van gegevens -, zelfs wanneer er geen netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="7ce4a-203">Offline sync allows end users toointeract with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
