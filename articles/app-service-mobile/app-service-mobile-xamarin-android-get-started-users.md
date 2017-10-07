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
# <a name="add-authentication-tooyour-xamarinandroid-app"></a><span data-ttu-id="e59cc-103">Verificatie tooyour Xamarin.Android-app toevoegen</span><span class="sxs-lookup"><span data-stu-id="e59cc-103">Add authentication tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="e59cc-104">Dit onderwerp leest u hoe tooauthenticate gebruikers van een mobiele App van uw clienttoepassing.</span><span class="sxs-lookup"><span data-stu-id="e59cc-104">This topic shows you how tooauthenticate users of a Mobile App from your client application.</span></span> <span data-ttu-id="e59cc-105">In deze zelfstudie maakt toevoegen u verificatie toohello Quick Start-project met behulp van een id-provider die wordt ondersteund door Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="e59cc-105">In this tutorial, you add authentication toohello quickstart project using an identity provider that is supported by Azure Mobile Apps.</span></span> <span data-ttu-id="e59cc-106">Nadat wordt hebt geverifieerd en gemachtigd in Hallo mobiele App, wordt Hallo gebruiker-ID-waarde weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e59cc-106">After being successfully authenticated and authorized in hello Mobile App, hello user ID value is displayed.</span></span>

<span data-ttu-id="e59cc-107">Deze zelfstudie is gebaseerd op Hallo mobiele App Quick Start.</span><span class="sxs-lookup"><span data-stu-id="e59cc-107">This tutorial is based on hello Mobile App quickstart.</span></span> <span data-ttu-id="e59cc-108">U moet ook eerst Hallo-zelfstudie hebt voltooid [een Xamarin.Android-app maken].</span><span class="sxs-lookup"><span data-stu-id="e59cc-108">You must also first complete hello tutorial [Create a Xamarin.Android app].</span></span> <span data-ttu-id="e59cc-109">Als u geen gebruik Hallo snel starten-serverproject gedownload, moet u Hallo verificatie pakket tooyour extensieproject toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e59cc-109">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="e59cc-110">Zie voor meer informatie over server extensiepakketten [werken met back-endserver voor Hallo .NET SDK voor Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="e59cc-110">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <span data-ttu-id="e59cc-111"><a name="register"></a>Uw app registreren voor verificatie en App-Services configureren</span><span class="sxs-lookup"><span data-stu-id="e59cc-111"><a name="register"></a>Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="e59cc-112"><a name="redirecturl"></a>Uw app toohello toegestane externe Omleidings-URL's toevoegen</span><span class="sxs-lookup"><span data-stu-id="e59cc-112"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="e59cc-113">Veilige verificatie vereist dat u een nieuwe URL-schema voor uw app definiëren.</span><span class="sxs-lookup"><span data-stu-id="e59cc-113">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="e59cc-114">Hierdoor Hallo verificatie system tooredirect back tooyour app zodra de Hallo verificatieproces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e59cc-114">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="e59cc-115">In deze zelfstudie gebruiken we Hallo URL-schema _appname_ in.</span><span class="sxs-lookup"><span data-stu-id="e59cc-115">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="e59cc-116">U kunt echter een URL-schema dat u kiest.</span><span class="sxs-lookup"><span data-stu-id="e59cc-116">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="e59cc-117">Deze moet uniek tooyour mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="e59cc-117">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="e59cc-118">Hallo-omleiding tooenable aan serverzijde Hallo:</span><span class="sxs-lookup"><span data-stu-id="e59cc-118">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="e59cc-119">Selecteer in de Hallo [Azure portal], uw App Service.</span><span class="sxs-lookup"><span data-stu-id="e59cc-119">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="e59cc-120">Klik op Hallo **verificatie / autorisatie** menuoptie.</span><span class="sxs-lookup"><span data-stu-id="e59cc-120">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="e59cc-121">In Hallo **toegestaan externe Omleidings-URL's**, voer `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="e59cc-121">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="e59cc-122">Hallo **url_scheme_of_your_app** in deze reeks is Hallo URL-schema voor uw mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="e59cc-122">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="e59cc-123">Deze moet voldoen aan de normale URL-specificatie voor een protocol (Gebruik letters en cijfers alleen en begin met een letter).</span><span class="sxs-lookup"><span data-stu-id="e59cc-123">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="e59cc-124">U moet een notitie van Hallo-tekenreeks die u kiest, want u tooadjust uw code mobiele toepassing Hello URL-schema op verschillende plaatsen moet.</span><span class="sxs-lookup"><span data-stu-id="e59cc-124">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="e59cc-125">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e59cc-125">Click **OK**.</span></span>

5. <span data-ttu-id="e59cc-126">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e59cc-126">Click **Save**.</span></span>

## <span data-ttu-id="e59cc-127"><a name="permissions"></a>Machtigingen tooauthenticated gebruikers beperken</span><span class="sxs-lookup"><span data-stu-id="e59cc-127"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="e59cc-128">Voer Hallo client-project op een apparaat of emulator in Visual Studio en Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="e59cc-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="e59cc-129">Controleer of dat een niet-verwerkte uitzondering met een statuscode van 401 (niet-geautoriseerd) treedt op nadat het Hallo-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="e59cc-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="e59cc-130">Dit gebeurt omdat Hallo app tooaccess backend voor mobiele Apps als een niet-geverifieerde gebruiker probeert.</span><span class="sxs-lookup"><span data-stu-id="e59cc-130">This happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="e59cc-131">Hallo *TodoItem* tabel nu is verificatie vereist.</span><span class="sxs-lookup"><span data-stu-id="e59cc-131">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="e59cc-132">Vervolgens wordt u Hallo client app toorequest resources uit de back-end van Hallo Mobile Apps bijwerken met een geverifieerde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="e59cc-132">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <span data-ttu-id="e59cc-133"><a name="add-authentication"></a>Verificatie toohello app toevoegen</span><span class="sxs-lookup"><span data-stu-id="e59cc-133"><a name="add-authentication"></a>Add authentication toohello app</span></span>
<span data-ttu-id="e59cc-134">Hallo-app is een bijgewerkte toorequire gebruikers tootap hello **aanmelden** knop en worden geverifieerd voordat gegevens worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e59cc-134">hello app is updated toorequire users tootap hello **Sign in** button and authenticate before data is displayed.</span></span>

1. <span data-ttu-id="e59cc-135">Hallo na code toohello toevoegen **TodoActivity** klasse:</span><span class="sxs-lookup"><span data-stu-id="e59cc-135">Add hello following code toohello **TodoActivity** class:</span></span>
   
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
   
    <span data-ttu-id="e59cc-136">Hiermee maakt u een nieuwe methode tooauthenticate een gebruiker en een methode-handler voor een nieuwe **aanmelden** knop.</span><span class="sxs-lookup"><span data-stu-id="e59cc-136">This creates a new method tooauthenticate a user and a method handler for a new **Sign in** button.</span></span> <span data-ttu-id="e59cc-137">Hallo-gebruiker in bovenstaande Hallo voorbeeldcode wordt geverifieerd met behulp van een Facebook-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e59cc-137">hello user in hello example code above is authenticated by using a Facebook login.</span></span> <span data-ttu-id="e59cc-138">Gebruikte toodisplay Hallo gebruikers-ID eenmaal is geverifieerd, is een dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e59cc-138">A dialog is used toodisplay hello user ID once authenticated.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e59cc-139">Als u van een id-provider dan Facebook gebruikmaakt, Hallo-waarde doorgegeven te wijzigen**LoginAsync** hierboven tooone van de volgende Hallo: *MicrosoftAccount*, *Twitter*, *Google*, of *WindowsAzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="e59cc-139">If you are using an identity provider other than Facebook, change hello value passed too**LoginAsync** above tooone of hello following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span></span>
   > 
   > 
2. <span data-ttu-id="e59cc-140">In Hallo **OnCreate** methode, verwijderen of commentarieer Hallo coderegel te volgen:</span><span class="sxs-lookup"><span data-stu-id="e59cc-140">In hello **OnCreate** method, delete or comment-out hello following line of code:</span></span>
   
        OnRefreshItemsSelected ();
3. <span data-ttu-id="e59cc-141">Voeg toe Hallo volgende Hallo Activity_To_Do.axml bestand *LoginUser* knop definitie voordat Hallo bestaande *AddItem* knop:</span><span class="sxs-lookup"><span data-stu-id="e59cc-141">In hello Activity_To_Do.axml file, add hello following *LoginUser* button definition before hello existing *AddItem* button:</span></span>
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. <span data-ttu-id="e59cc-142">Hallo volgende element toohello Strings.xml resources toevoegen:</span><span class="sxs-lookup"><span data-stu-id="e59cc-142">Add hello following element toohello Strings.xml resources file:</span></span>
   
        <string name="login_button_text">Sign in</string>
5. <span data-ttu-id="e59cc-143">Hallo AndroidManifest.xml bestand openen, toevoegen Hallo-code in volgende `<application>` XML-element:</span><span class="sxs-lookup"><span data-stu-id="e59cc-143">Open hello AndroidManifest.xml file, add hello following code inside `<application>` XML element:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. <span data-ttu-id="e59cc-144">In Visual Studio en Xamarin Studio Hallo client-project uitvoeren op een apparaat of emulator en meld u aan met uw gekozen id-provider.</span><span class="sxs-lookup"><span data-stu-id="e59cc-144">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator and sign in with your chosen identity provider.</span></span> <span data-ttu-id="e59cc-145">Wanneer u is aangemeld bent, Hallo app uw aanmeldings-ID wordt weergegeven en Hallo lijst met todo-items en u kunt updates toohello gegevens maken.</span><span class="sxs-lookup"><span data-stu-id="e59cc-145">When you are successfully logged-in, hello app will display your login ID and hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[een Xamarin.Android-app maken]: app-service-mobile-xamarin-android-get-started.md