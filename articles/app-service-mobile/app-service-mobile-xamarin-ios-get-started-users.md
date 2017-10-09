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
# <a name="add-authentication-tooyour-xamarinios-app"></a><span data-ttu-id="fc54e-103">Verificatie tooyour Xamarin.iOS-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="fc54e-103">Add authentication tooyour Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="fc54e-104">Dit onderwerp leest u hoe tooauthenticate gebruikers van een App Service Mobile App van uw clienttoepassing.</span><span class="sxs-lookup"><span data-stu-id="fc54e-104">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="fc54e-105">In deze zelfstudie voegt u verificatie toohello Xamarin.iOS Quick Start-project met behulp van een id-provider die wordt ondersteund door App Service.</span><span class="sxs-lookup"><span data-stu-id="fc54e-105">In this tutorial, you add authentication toohello Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="fc54e-106">Nadat wordt is geverifieerd en geautoriseerd door uw mobiele App, Hallo gebruiker-ID-waarde wordt weergegeven en kunt u gegevens in een tabel staat tooaccess beperkt.</span><span class="sxs-lookup"><span data-stu-id="fc54e-106">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed and you will be able tooaccess restricted table data.</span></span>

<span data-ttu-id="fc54e-107">U moet eerst Hallo-zelfstudie hebt voltooid [een Xamarin.iOS-app maken].</span><span class="sxs-lookup"><span data-stu-id="fc54e-107">You must first complete hello tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="fc54e-108">Als u geen gebruik Hallo snel starten-serverproject gedownload, moet u Hallo verificatie pakket tooyour extensieproject toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fc54e-108">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="fc54e-109">Zie voor meer informatie over server extensiepakketten [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="fc54e-109">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="fc54e-110">Uw app registreren voor verificatie en App-Services configureren</span><span class="sxs-lookup"><span data-stu-id="fc54e-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a><span data-ttu-id="fc54e-111">Uw app toohello toegestane externe Omleidings-URL's toevoegen</span><span class="sxs-lookup"><span data-stu-id="fc54e-111">Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="fc54e-112">Veilige verificatie vereist dat u een nieuwe URL-schema voor uw app definiëren.</span><span class="sxs-lookup"><span data-stu-id="fc54e-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="fc54e-113">Hierdoor Hallo verificatie system tooredirect back tooyour app zodra de Hallo verificatieproces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="fc54e-113">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="fc54e-114">In deze zelfstudie gebruiken we Hallo URL-schema _appname_ in.</span><span class="sxs-lookup"><span data-stu-id="fc54e-114">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="fc54e-115">U kunt echter een URL-schema dat u kiest.</span><span class="sxs-lookup"><span data-stu-id="fc54e-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="fc54e-116">Deze moet uniek tooyour mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="fc54e-116">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="fc54e-117">Hallo-omleiding tooenable aan serverzijde Hallo:</span><span class="sxs-lookup"><span data-stu-id="fc54e-117">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="fc54e-118">Selecteer in de Hallo [Azure portal], uw App Service.</span><span class="sxs-lookup"><span data-stu-id="fc54e-118">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="fc54e-119">Klik op Hallo **verificatie / autorisatie** menuoptie.</span><span class="sxs-lookup"><span data-stu-id="fc54e-119">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="fc54e-120">In Hallo **toegestaan externe Omleidings-URL's**, voer `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="fc54e-120">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="fc54e-121">Hallo **url_scheme_of_your_app** in deze reeks is Hallo URL-schema voor uw mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="fc54e-121">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="fc54e-122">Deze moet voldoen aan de normale URL-specificatie voor een protocol (Gebruik letters en cijfers alleen en begin met een letter).</span><span class="sxs-lookup"><span data-stu-id="fc54e-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="fc54e-123">U moet een notitie van Hallo-tekenreeks die u kiest, want u tooadjust uw code mobiele toepassing Hello URL-schema op verschillende plaatsen moet.</span><span class="sxs-lookup"><span data-stu-id="fc54e-123">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="fc54e-124">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="fc54e-124">Click **OK**.</span></span>

5. <span data-ttu-id="fc54e-125">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="fc54e-125">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="fc54e-126">Machtigingen tooauthenticated gebruikers beperken</span><span class="sxs-lookup"><span data-stu-id="fc54e-126">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="fc54e-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="fc54e-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="fc54e-128">Voer Hallo client-project op een apparaat of emulator in Visual Studio en Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="fc54e-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="fc54e-129">Controleer of dat een niet-verwerkte uitzondering met een statuscode van 401 (niet-geautoriseerd) treedt op nadat het Hallo-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="fc54e-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="fc54e-130">Hallo mislukte is vastgelegd toohello console van Hallo foutopsporingsprogramma.</span><span class="sxs-lookup"><span data-stu-id="fc54e-130">hello failure is logged toohello console of hello debugger.</span></span> <span data-ttu-id="fc54e-131">Dus in Visual Studio ziet u fout in het uitvoervenster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="fc54e-131">So in Visual Studio, you should see hello failure in hello output window.</span></span>

<span data-ttu-id="fc54e-132">&nbsp;&nbsp;Deze onbevoegde fout treedt op omdat het Hallo-app probeert tooaccess backend voor mobiele Apps als een niet-geverifieerde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="fc54e-132">&nbsp;&nbsp;This unauthorized failure happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="fc54e-133">Hallo *TodoItem* tabel nu is verificatie vereist.</span><span class="sxs-lookup"><span data-stu-id="fc54e-133">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="fc54e-134">Vervolgens wordt u Hallo client app toorequest resources uit de back-end van Hallo Mobile Apps bijwerken met een geverifieerde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="fc54e-134">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="fc54e-135">Verificatie toohello app toevoegen</span><span class="sxs-lookup"><span data-stu-id="fc54e-135">Add authentication toohello app</span></span>
<span data-ttu-id="fc54e-136">In deze sectie wijzigt u Hallo app toodisplay een aanmeldingsscherm voordat gegevens worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fc54e-136">In this section, you will modify hello app toodisplay a login screen before displaying data.</span></span> <span data-ttu-id="fc54e-137">Wanneer Hallo-app wordt gestart, niet niet verbinding maakt tooyour App Service en gegevens kunnen niet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fc54e-137">When hello app starts, it will not not connect tooyour App Service and will not display any data.</span></span> <span data-ttu-id="fc54e-138">Na de eerste keer Hallo voert die gebruiker Hallo gebaar voor het vernieuwen van Hallo Hallo aanmeldingsscherm wordt weergegeven; na een geslaagde aanmelding wordt hello lijst met todo-items weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fc54e-138">After hello first time that hello user performs hello refresh gesture, hello login screen will appear; after successful login hello list of todo items will be displayed.</span></span>

1. <span data-ttu-id="fc54e-139">Open in Hallo clientproject Hallo-bestand **QSTodoService.cs** en voeg de volgende Hallo gebruiksinstructie en `MobileServiceUser` met accessor toohello QSTodoService klasse:</span><span class="sxs-lookup"><span data-stu-id="fc54e-139">In hello client project, open hello file **QSTodoService.cs** and add hello following using statement and `MobileServiceUser` with accessor toohello QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="fc54e-140">Met de naam van de nieuwe methode Add **verifiëren** te**QSTodoService** Hello definitie te volgen:</span><span class="sxs-lookup"><span data-stu-id="fc54e-140">Add new method named **Authenticate** too**QSTodoService** with hello following definition:</span></span>

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

    >[AZURE.NOTE] <span data-ttu-id="fc54e-141">Als u van een id-provider dan een Facebook gebruikmaakt, Hallo-waarde doorgegeven te wijzigen**LoginAsync** hierboven tooone van de volgende Hallo: _MicrosoftAccount_, _Twitter_, _Google_, of _WindowsAzureActiveDirectory_.</span><span class="sxs-lookup"><span data-stu-id="fc54e-141">If you are using an identity provider other than a Facebook, change hello value passed too**LoginAsync** above tooone of hello following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="fc54e-142">Open **QSTodoListViewController.cs**.</span><span class="sxs-lookup"><span data-stu-id="fc54e-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="fc54e-143">Hallo-methodedefinitie van wijzigen **ViewDidLoad** Hallo aanroep te verwijderen**RefreshAsync()** bijna Hallo einde:</span><span class="sxs-lookup"><span data-stu-id="fc54e-143">Modify hello method definition of **ViewDidLoad** removing hello call too**RefreshAsync()** near hello end:</span></span>
   
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
4. <span data-ttu-id="fc54e-144">Hallo-methode Modify **RefreshAsync** tooauthenticate als hello **gebruiker** eigenschap is null.</span><span class="sxs-lookup"><span data-stu-id="fc54e-144">Modify hello method **RefreshAsync** tooauthenticate if hello **User** property is null.</span></span> <span data-ttu-id="fc54e-145">Hallo code Hallo boven aan het Hallo-methodedefinitie volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="fc54e-145">Add hello following code at hello top of hello method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="fc54e-146">Open **AppDelegate.cs**, Hallo methode volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="fc54e-146">Open **AppDelegate.cs**, add hello following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="fc54e-147">Open **Info.plist** bestand, te navigeren**URL typen** in Hallo **Geavanceerd** sectie.</span><span class="sxs-lookup"><span data-stu-id="fc54e-147">Open **Info.plist** file, navigate too**URL Types** in hello **Advanced** section.</span></span> <span data-ttu-id="fc54e-148">Nu configureren Hallo **id** en Hallo **URL-schema's** van uw URL-Type en klik op **URL-Type toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="fc54e-148">Now configure hello **Identifier** and hello **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="fc54e-149">**URL-schema's** moet dezelfde Hallo als uw {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="fc54e-149">**URL Schemes** should be hello same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="fc54e-150">In Visual Studio of Xamarin Studio verbonden tooyour Xamarin bouwen Host op uw Mac Hallo clientproject die gericht is op een apparaat of emulator uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fc54e-150">In Visual Studio or Xamarin Studio connected tooyour Xamarin Build Host on your Mac, run hello client project targeting a device or emulator.</span></span> <span data-ttu-id="fc54e-151">Controleer of u dat die app Hallo geen gegevens weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fc54e-151">Verify that hello app displays no data.</span></span>
   
    <span data-ttu-id="fc54e-152">Hallo vernieuwen gebaar door binnen te halen omlaag Hallo lijst met items, waardoor de Hallo aanmelding scherm tooappear uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fc54e-152">Perform hello refresh gesture by pulling down hello list of items, which will cause hello login screen tooappear.</span></span> <span data-ttu-id="fc54e-153">Zodra u geldige referenties hebt, Hallo app Hallo-lijst van todo-items worden weergegeven en kunt u updates toohello gegevens maken.</span><span class="sxs-lookup"><span data-stu-id="fc54e-153">Once you have successfully entered valid credentials, hello app will display hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[een Xamarin.iOS-app maken]: app-service-mobile-xamarin-ios-get-started.md