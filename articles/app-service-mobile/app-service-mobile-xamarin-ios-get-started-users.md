---
title: Aan de slag met verificatie voor mobiele Apps in Xamarin voor iOS
description: "Informatie over het verifiëren van gebruikers van uw Xamarin iOS-app via een groot aantal identiteitsproviders, waaronder AAD, Google, Facebook, Twitter en Microsoft met Mobile Apps."
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
ms.openlocfilehash: 454b2df5a9bf8cfba93befea54370957ab044d95
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-xamarinios-app"></a><span data-ttu-id="070bc-103">Authenticatie toevoegen aan uw Xamarin.iOS-app</span><span class="sxs-lookup"><span data-stu-id="070bc-103">Add authentication to your Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="070bc-104">Dit onderwerp leest u hoe u verifieert gebruikers van een App Service Mobile App van uw clienttoepassing.</span><span class="sxs-lookup"><span data-stu-id="070bc-104">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="070bc-105">In deze zelfstudie kunt u verificatie toevoegen aan het Xamarin.iOS-Quick Start-project met een id-provider die wordt ondersteund door App Service.</span><span class="sxs-lookup"><span data-stu-id="070bc-105">In this tutorial, you add authentication to the Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="070bc-106">Nadat wordt is geverifieerd en geautoriseerd door uw mobiele App, de waarde van de gebruiker-ID wordt weergegeven en kunt u zich toegang kunnen krijgen tot gegevens in een tabel met beperkte toegang.</span><span class="sxs-lookup"><span data-stu-id="070bc-106">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed and you will be able to access restricted table data.</span></span>

<span data-ttu-id="070bc-107">U moet eerst Voltooi de zelfstudie [een Xamarin.iOS-app maken].</span><span class="sxs-lookup"><span data-stu-id="070bc-107">You must first complete the tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="070bc-108">Als u het gedownloade quick start-serverproject niet gebruikt, moet u het pakket voor verificatie-extensie toevoegen aan uw project.</span><span class="sxs-lookup"><span data-stu-id="070bc-108">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="070bc-109">Zie voor meer informatie over server extensiepakketten [werken met de .NET-back-endserver SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="070bc-109">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="070bc-110">Uw app registreren voor verificatie en App-Services configureren</span><span class="sxs-lookup"><span data-stu-id="070bc-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-to-the-allowed-external-redirect-urls"></a><span data-ttu-id="070bc-111">Uw app toevoegen aan de toegestane externe Omleidings-URL 's</span><span class="sxs-lookup"><span data-stu-id="070bc-111">Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="070bc-112">Veilige verificatie vereist dat u een nieuwe URL-schema voor uw app definiëren.</span><span class="sxs-lookup"><span data-stu-id="070bc-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="070bc-113">Hierdoor kan de verificatiesysteem terug te keren naar uw app zodra het verificatieproces voltooid is.</span><span class="sxs-lookup"><span data-stu-id="070bc-113">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="070bc-114">In deze zelfstudie gebruiken we het URL-schema _appname_ in.</span><span class="sxs-lookup"><span data-stu-id="070bc-114">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="070bc-115">U kunt echter een URL-schema dat u kiest.</span><span class="sxs-lookup"><span data-stu-id="070bc-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="070bc-116">Deze moet uniek zijn voor uw mobiele App.</span><span class="sxs-lookup"><span data-stu-id="070bc-116">It should be unique to your mobile application.</span></span> <span data-ttu-id="070bc-117">De omleiding op de server inschakelen:</span><span class="sxs-lookup"><span data-stu-id="070bc-117">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="070bc-118">Selecteer in de [Azure-portal] uw App Service.</span><span class="sxs-lookup"><span data-stu-id="070bc-118">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="070bc-119">Klik op de **verificatie / autorisatie** menuoptie.</span><span class="sxs-lookup"><span data-stu-id="070bc-119">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="070bc-120">In de **toegestaan externe Omleidings-URL's**, voer `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="070bc-120">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="070bc-121">De **url_scheme_of_your_app** in deze tekenreeks wordt het URL-schema voor uw mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="070bc-121">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="070bc-122">Deze moet voldoen aan de normale URL-specificatie voor een protocol (Gebruik letters en cijfers alleen en begin met een letter).</span><span class="sxs-lookup"><span data-stu-id="070bc-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="070bc-123">U moet een notitie van de tekenreeks die u naar wens aanpassen van uw mobiele toepassingscode met het URL-schema op verschillende plaatsen.</span><span class="sxs-lookup"><span data-stu-id="070bc-123">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="070bc-124">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="070bc-124">Click **OK**.</span></span>

5. <span data-ttu-id="070bc-125">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="070bc-125">Click **Save**.</span></span>

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="070bc-126">Machtigingen beperken voor geverifieerde gebruikers</span><span class="sxs-lookup"><span data-stu-id="070bc-126">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="070bc-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="070bc-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="070bc-128">Voer het clientproject op een apparaat of emulator in Visual Studio en Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="070bc-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="070bc-129">Controleer of dat een niet-verwerkte uitzondering met een statuscode van 401 (niet-geautoriseerd) treedt op nadat de app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="070bc-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="070bc-130">De fout wordt geregistreerd in de console van het foutopsporingsprogramma.</span><span class="sxs-lookup"><span data-stu-id="070bc-130">The failure is logged to the console of the debugger.</span></span> <span data-ttu-id="070bc-131">Dus in Visual Studio ziet u de fout in het uitvoervenster.</span><span class="sxs-lookup"><span data-stu-id="070bc-131">So in Visual Studio, you should see the failure in the output window.</span></span>

<span data-ttu-id="070bc-132">&nbsp;&nbsp;Deze onbevoegde fout treedt op omdat de app probeert te krijgen tot uw back-end voor mobiele App als een niet-geverifieerde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="070bc-132">&nbsp;&nbsp;This unauthorized failure happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="070bc-133">De *TodoItem* tabel nu is verificatie vereist.</span><span class="sxs-lookup"><span data-stu-id="070bc-133">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="070bc-134">U wordt vervolgens de client-app voor aanvragen voor resources bijwerken vanuit de back-end voor de mobiele App met een geverifieerde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="070bc-134">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-to-the-app"></a><span data-ttu-id="070bc-135">Verificatie toevoegen aan de app.</span><span class="sxs-lookup"><span data-stu-id="070bc-135">Add authentication to the app</span></span>
<span data-ttu-id="070bc-136">In deze sectie wijzigt u de app voor een aanmeldingsscherm weergegeven voordat gegevens worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="070bc-136">In this section, you will modify the app to display a login screen before displaying data.</span></span> <span data-ttu-id="070bc-137">Wanneer de app wordt gestart, wordt geen geen verbinding maken met uw App Service en gegevens kunnen niet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="070bc-137">When the app starts, it will not not connect to your App Service and will not display any data.</span></span> <span data-ttu-id="070bc-138">Nadat de eerste keer dat de gebruiker uitvoert de gebaar vernieuwen van het aanmeldingsscherm weergegeven; na een geslaagde aanmelding wordt de lijst met todo-items worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="070bc-138">After the first time that the user performs the refresh gesture, the login screen will appear; after successful login the list of todo items will be displayed.</span></span>

1. <span data-ttu-id="070bc-139">Open het bestand in het clientproject **QSTodoService.cs** en voeg de volgende gebruiksinstructie en `MobileServiceUser` met accessor aan de klasse QSTodoService:</span><span class="sxs-lookup"><span data-stu-id="070bc-139">In the client project, open the file **QSTodoService.cs** and add the following using statement and `MobileServiceUser` with accessor to the QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="070bc-140">Met de naam van de nieuwe methode Add **verifiëren** naar **QSTodoService** met de definitie van de volgende:</span><span class="sxs-lookup"><span data-stu-id="070bc-140">Add new method named **Authenticate** to **QSTodoService** with the following definition:</span></span>

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

    >[AZURE.NOTE] <span data-ttu-id="070bc-141">Als u van een id-provider dan een Facebook gebruikmaakt, wijzig de waarde die is doorgegeven aan **LoginAsync** boven op een van de volgende opties: _MicrosoftAccount_, _Twitter_, _Google_, of _WindowsAzureActiveDirectory_.</span><span class="sxs-lookup"><span data-stu-id="070bc-141">If you are using an identity provider other than a Facebook, change the value passed to **LoginAsync** above to one of the following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="070bc-142">Open **QSTodoListViewController.cs**.</span><span class="sxs-lookup"><span data-stu-id="070bc-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="070bc-143">Wijzig de methodedefinitie van **ViewDidLoad** verwijderen van de aanroep van **RefreshAsync()** in de buurt van het einde:</span><span class="sxs-lookup"><span data-stu-id="070bc-143">Modify the method definition of **ViewDidLoad** removing the call to **RefreshAsync()** near the end:</span></span>
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out the call to RefreshAsync
            // await RefreshAsync();
        }
4. <span data-ttu-id="070bc-144">De methode wijzigen **RefreshAsync** om te verifiëren als de **gebruiker** eigenschap is null.</span><span class="sxs-lookup"><span data-stu-id="070bc-144">Modify the method **RefreshAsync** to authenticate if the **User** property is null.</span></span> <span data-ttu-id="070bc-145">Voeg de volgende code aan de bovenkant van de methodedefinitie van de:</span><span class="sxs-lookup"><span data-stu-id="070bc-145">Add the following code at the top of the method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="070bc-146">Open **AppDelegate.cs**, voeg de volgende methode toe:</span><span class="sxs-lookup"><span data-stu-id="070bc-146">Open **AppDelegate.cs**, add the following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="070bc-147">Open **Info.plist** bestand, gaat u naar **URL typen** in de **Geavanceerd** sectie.</span><span class="sxs-lookup"><span data-stu-id="070bc-147">Open **Info.plist** file, navigate to **URL Types** in the **Advanced** section.</span></span> <span data-ttu-id="070bc-148">Nu configureren de **id** en de **URL-schema's** van uw URL-Type en klik op **URL-Type toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="070bc-148">Now configure the **Identifier** and the **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="070bc-149">**URL-schema's** moet hetzelfde zijn als uw {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="070bc-149">**URL Schemes** should be the same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="070bc-150">In Visual Studio of Xamarin Studio verbonden met uw Host Xamarin bouwen op uw Mac het clientproject die gericht is op een apparaat of emulator uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="070bc-150">In Visual Studio or Xamarin Studio connected to your Xamarin Build Host on your Mac, run the client project targeting a device or emulator.</span></span> <span data-ttu-id="070bc-151">Controleer of dat de app geen gegevens weergegeven.</span><span class="sxs-lookup"><span data-stu-id="070bc-151">Verify that the app displays no data.</span></span>
   
    <span data-ttu-id="070bc-152">Een gebaar van de vernieuwing uitvoeren met het binnenhalen van de lijst met items, waardoor het aanmeldingsscherm wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="070bc-152">Perform the refresh gesture by pulling down the list of items, which will cause the login screen to appear.</span></span> <span data-ttu-id="070bc-153">Nadat u geldige referenties hebt, de app wordt weergegeven de lijst met todo-items en kunt u updates aanbrengen in de gegevens.</span><span class="sxs-lookup"><span data-stu-id="070bc-153">Once you have successfully entered valid credentials, the app will display the list of todo items, and you can make updates to the data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
<span data-ttu-id="070bc-154">[een Xamarin.iOS-app maken]: app-service-mobile-xamarin-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="070bc-154">[Create a Xamarin.iOS app]: app-service-mobile-xamarin-ios-get-started.md</span></span>