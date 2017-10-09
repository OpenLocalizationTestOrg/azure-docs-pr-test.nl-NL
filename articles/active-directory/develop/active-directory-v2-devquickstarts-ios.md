---
title: aaaAdd tooan-in iOS-toepassing met behulp van Azure AD v2.0-eindpunt Hallo | Microsoft Docs
description: Hoe toobuild een iOS-app die meldt zich aan gebruikers met beide persoonlijke Microsoft-account en werk-of schoolaccounts met behulp van de bibliotheken van derden.
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: a384062e6e4bd398a2b12318800728e627e05c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="8973f-103">Aanmelden tooan iOS-app met behulp van een derde partij-bibliotheek met Graph API met behulp van Hallo v2.0-eindpunt toevoegen</span><span class="sxs-lookup"><span data-stu-id="8973f-103">Add sign-in tooan iOS app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="8973f-104">Hallo Microsoft identity-platform gebruikt open standaarden, zoals OAuth2 en OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="8973f-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="8973f-105">Ontwikkelaars kunnen een bibliotheek, ze toointegrate met onze services willen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8973f-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="8973f-106">ons platform toohelp ontwikkelaars gebruiken met andere bibliotheken, hebben we hoe de enkele scenario's zoals deze één toodemonstrate geschreven tooconfigure van derden bibliotheken tooconnect toohello Microsoft identity-platform.</span><span class="sxs-lookup"><span data-stu-id="8973f-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="8973f-107">De meeste bibliotheken die implementeren [hello RFC6749 OAuth2-specificatie](https://tools.ietf.org/html/rfc6749) verbinding kunnen maken van toohello Microsoft identity-platform.</span><span class="sxs-lookup"><span data-stu-id="8973f-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="8973f-108">Hallo-toepassing die in dit scenario maakt, kunnen gebruikers aanmelden tootheir organisatie en zoekt u naar anderen binnen hun organisatie met behulp van Hallo Graph API.</span><span class="sxs-lookup"><span data-stu-id="8973f-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for others in their organization by using hello Graph API.</span></span>

<span data-ttu-id="8973f-109">Als u nieuwe tooOAuth2 of OpenID Connect, kan veel van deze voorbeeldconfiguratie zin tooyou niet maken.</span><span class="sxs-lookup"><span data-stu-id="8973f-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="8973f-110">Het is raadzaam dat u leest [v2.0-protocollen - stromen van OAuth 2.0 autorisatie Code](active-directory-v2-protocols-oauth-code.md) voor de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="8973f-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="8973f-111">Sommige functies van ons platform waarvoor een expressie in Hallo OAuth2 of OpenID Connect standaarden, zoals voorwaardelijke toegang en beheer van Intune vereist u toouse onze open-source bibliotheken voor Microsoft Azure identiteit.</span><span class="sxs-lookup"><span data-stu-id="8973f-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="8973f-112">Hallo v2.0-eindpunt biedt geen ondersteuning voor alle Azure Active Directory-scenario's en onderdelen.</span><span class="sxs-lookup"><span data-stu-id="8973f-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="8973f-113">toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="8973f-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="8973f-114">Code vanuit GitHub downloaden</span><span class="sxs-lookup"><span data-stu-id="8973f-114">Download code from GitHub</span></span>
<span data-ttu-id="8973f-115">Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span><span class="sxs-lookup"><span data-stu-id="8973f-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="8973f-116">toofollow langs, kunt u [basis van Hallo app downloaden als een ZIP-](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) of kloon Hallo basisproject:</span><span class="sxs-lookup"><span data-stu-id="8973f-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="8973f-117">U kunt ook gewoon Hallo voorbeeld downloaden en meteen aan de slag:</span><span class="sxs-lookup"><span data-stu-id="8973f-117">You can also just download hello sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="8973f-118">Een app registreren</span><span class="sxs-lookup"><span data-stu-id="8973f-118">Register an app</span></span>
<span data-ttu-id="8973f-119">Maak een nieuwe app op Hallo [toepassing registratieportal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of volgen gedetailleerde stappen op Hallo [hoe tooregister een app met Hallo v2.0-eindpunt](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="8973f-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at  [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="8973f-120">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="8973f-120">Make sure to:</span></span>

* <span data-ttu-id="8973f-121">Kopiëren Hallo **toepassings-Id** die is toegewezen tooyour app omdat u hebt deze snel nodig.</span><span class="sxs-lookup"><span data-stu-id="8973f-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="8973f-122">Hallo toevoegen **Mobile** platform voor uw app.</span><span class="sxs-lookup"><span data-stu-id="8973f-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="8973f-123">Kopiëren Hallo **omleidings-URI** van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="8973f-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="8973f-124">Moet u de standaardwaarde Hallo van `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="8973f-124">You must use hello default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="8973f-125">Hallo van derden NXOAuth2 bibliotheek downloaden en een werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="8973f-125">Download hello third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="8973f-126">Voor dit scenario moet u Hallo OAuth2Client vanuit GitHub, namelijk een OAuth2-bibliotheek voor Mac OS X- en iOS (Cocoa en Cocoa touch) gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8973f-126">For this walkthrough, you will use hello OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="8973f-127">Deze bibliotheek is gebaseerd op concept 10 van Hallo OAuth2-specificatie. Hallo systeemeigen toepassingsprofiel implementeert en ondersteunt Hallo autorisatie endpoint van Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8973f-127">This library is based on draft 10 of hello OAuth2 spec. It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="8973f-128">Dit zijn alles van hello, moet u toointegrate met Hallo Microsoft identiteitsplatform.</span><span class="sxs-lookup"><span data-stu-id="8973f-128">These are all hello things you'll need toointegrate with hello Microsoft identity platform.</span></span>

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a><span data-ttu-id="8973f-129">Hallo-bibliotheek tooyour project via CocoaPods toevoegen</span><span class="sxs-lookup"><span data-stu-id="8973f-129">Add hello library tooyour project by using CocoaPods</span></span>
<span data-ttu-id="8973f-130">CocoaPods is een hulpmiddel voor afhankelijkheidsbeheer voor Xcode-projecten.</span><span class="sxs-lookup"><span data-stu-id="8973f-130">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="8973f-131">Het beheert vorige installatiestappen Hallo automatisch.</span><span class="sxs-lookup"><span data-stu-id="8973f-131">It manages hello previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="8973f-132">Hallo toothis podfile volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="8973f-132">Add hello following toothis podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="8973f-133">Hallo podfile laden via CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="8973f-133">Load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="8973f-134">Hiermee maakt u een nieuwe Xcode-werkruimte die u gaat laden.</span><span class="sxs-lookup"><span data-stu-id="8973f-134">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a><span data-ttu-id="8973f-135">Hallo-structuur van Hallo project verkennen</span><span class="sxs-lookup"><span data-stu-id="8973f-135">Explore hello structure of hello project</span></span>
<span data-ttu-id="8973f-136">Hallo structuur te volgen is voor onze project in Hallo basisproject ingesteld:</span><span class="sxs-lookup"><span data-stu-id="8973f-136">hello following structure is set up for our project in hello skeleton:</span></span>

* <span data-ttu-id="8973f-137">Een Master-weergave met een zoekopdracht UPN</span><span class="sxs-lookup"><span data-stu-id="8973f-137">A Master View with a UPN Search</span></span>
* <span data-ttu-id="8973f-138">Een detailweergave voor Hallo gegevens over de geselecteerde gebruiker Hallo</span><span class="sxs-lookup"><span data-stu-id="8973f-138">A Detail View for hello data about hello selected user</span></span>
* <span data-ttu-id="8973f-139">Een aanmelding weergave waar een gebruiker zich in toohello app tooquery Hallo grafiek aanmelden kunt</span><span class="sxs-lookup"><span data-stu-id="8973f-139">A Login View where a user can sign in toohello app tooquery hello graph</span></span>

<span data-ttu-id="8973f-140">We wordt toovarious bestanden in Hallo geraamte tooadd verificatie verplaatst.</span><span class="sxs-lookup"><span data-stu-id="8973f-140">We will move toovarious files in hello skeleton tooadd authentication.</span></span> <span data-ttu-id="8973f-141">Andere onderdelen van Hallo code, zoals visual code hello, tooidentity niet van toepassing zijn, maar zijn beschikbaar voor u.</span><span class="sxs-lookup"><span data-stu-id="8973f-141">Other parts of hello code, such as hello visual code, do not pertain tooidentity but are provided for you.</span></span>

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a><span data-ttu-id="8973f-142">Hallo settings.plst bestand instelt op Hallo-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="8973f-142">Set up hello settings.plst file in hello library</span></span>
* <span data-ttu-id="8973f-143">Open in Hallo Quick Start-project, Hallo `settings.plist` bestand.</span><span class="sxs-lookup"><span data-stu-id="8973f-143">In hello QuickStart project, open hello `settings.plist` file.</span></span> <span data-ttu-id="8973f-144">Vervang de waarden Hallo Hallo-elementen in Hallo sectie tooreflect Hallo waarden die u in hello Azure-portal gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8973f-144">Replace hello values of hello elements in hello section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="8973f-145">Uw code zal naar deze waarden verwijzen wanneer Hallo Active Directory Authentication Library wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8973f-145">Your code will reference these values whenever it uses hello Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="8973f-146">Hallo `clientId` Hallo client-ID van uw toepassing die u hebt gekopieerd uit de portal Hallo is.</span><span class="sxs-lookup"><span data-stu-id="8973f-146">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="8973f-147">Hallo `redirectUri` Hallo Omleidings-URL die Hallo portal opgegeven is.</span><span class="sxs-lookup"><span data-stu-id="8973f-147">hello `redirectUri` is hello redirect URL that hello portal provided.</span></span>

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="8973f-148">Hallo NXOAuth2Client bibliotheek in uw LoginViewController instellen</span><span class="sxs-lookup"><span data-stu-id="8973f-148">Set up hello NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="8973f-149">Hallo NXOAuth2Client bibliotheek is vereist voor sommige waarden tooget instellen.</span><span class="sxs-lookup"><span data-stu-id="8973f-149">hello NXOAuth2Client library requires some values tooget set up.</span></span> <span data-ttu-id="8973f-150">Nadat u die taak hebt voltooid, kunt u Hallo verkregen token toocall Hallo Graph API.</span><span class="sxs-lookup"><span data-stu-id="8973f-150">After you complete that task, you can use hello acquired token toocall hello Graph API.</span></span> <span data-ttu-id="8973f-151">Omdat `LoginView` moet op elk gewenst moment worden aangeroepen moeten we tooauthenticate, is het zinvol tooput configuratiewaarden in toothat-bestand.</span><span class="sxs-lookup"><span data-stu-id="8973f-151">Because `LoginView` will be called any time we need tooauthenticate, it makes sense tooput configuration values in toothat file.</span></span>

* <span data-ttu-id="8973f-152">We voegen sommige waarden toohello `LoginViewController.m` bestand tooset Hallo context voor verificatie en autorisatie.</span><span class="sxs-lookup"><span data-stu-id="8973f-152">Let's add some values toohello  `LoginViewController.m` file tooset hello context for authentication and authorization.</span></span> <span data-ttu-id="8973f-153">Meer informatie over Hallo waarden Volg Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="8973f-153">Details about hello values follow hello code.</span></span>
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

<span data-ttu-id="8973f-154">Bekijk meer informatie over het Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="8973f-154">Let's look at details about hello code.</span></span>

<span data-ttu-id="8973f-155">de eerste tekenreeks Hallo is voor `scopes`.</span><span class="sxs-lookup"><span data-stu-id="8973f-155">hello first string is for `scopes`.</span></span>  <span data-ttu-id="8973f-156">Hallo `User.Read` waarde kunt u tooread Hallo basisprofiel Hallo gebruiker aangemeld.</span><span class="sxs-lookup"><span data-stu-id="8973f-156">hello `User.Read` value allows you tooread hello basic profile of hello signed in user.</span></span>

<span data-ttu-id="8973f-157">U kunt meer informatie over alle beschikbare Hallo-scopes op [Microsoft Graph-machtigingsbereiken](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="8973f-157">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="8973f-158">Voor `authURL`, `loginURL`, `bhh`, en `tokenURL`, moet u eerder opgegeven Hallo-waarden.</span><span class="sxs-lookup"><span data-stu-id="8973f-158">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use hello values provided previously.</span></span> <span data-ttu-id="8973f-159">Als u Hallo open-source bibliotheken voor Microsoft Azure identiteit gebruikt, halen we deze gegevens voor u met behulp van onze metagegevenseindpunt.</span><span class="sxs-lookup"><span data-stu-id="8973f-159">If you use hello open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="8973f-160">We hebt Hallo harde werk van het extraheren van deze waarden voor u gedaan.</span><span class="sxs-lookup"><span data-stu-id="8973f-160">We've done hello hard work of extracting these values for you.</span></span>

<span data-ttu-id="8973f-161">Hallo `keychain` waarde is het Hallo-container die Hallo NXOAuth2Client bibliotheek gebruikt een toostore sleutelhanger toocreate uw tokens.</span><span class="sxs-lookup"><span data-stu-id="8973f-161">hello `keychain` value is hello container that hello NXOAuth2Client library will use toocreate a keychain toostore your tokens.</span></span> <span data-ttu-id="8973f-162">Als u tooget eenmalige aanmelding (SSO) via talrijke apps wilt, kunt u dezelfde sleutelhanger in elk van uw toepassingen Hallo en aanvragen Hallo gebruik van die sleutelhanger in uw Xcode-rechten.</span><span class="sxs-lookup"><span data-stu-id="8973f-162">If you'd like tooget single sign-on (SSO) across numerous apps, you can specify hello same keychain in each of your applications and request hello use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="8973f-163">Dit wordt uitgelegd in Hallo Apple-documentatie.</span><span class="sxs-lookup"><span data-stu-id="8973f-163">This is explained in hello Apple documentation.</span></span>

<span data-ttu-id="8973f-164">Hallo rest van deze waarden zijn vereiste toouse Hallo-bibliotheek en locaties voor u toocarry waarden toohello context.</span><span class="sxs-lookup"><span data-stu-id="8973f-164">hello rest of these values are required toouse hello library and create places for you toocarry values toohello context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="8973f-165">Een URL-cache maken</span><span class="sxs-lookup"><span data-stu-id="8973f-165">Create a URL cache</span></span>
<span data-ttu-id="8973f-166">Binnen `(void)viewDidLoad()`, die altijd wordt aangeroepen nadat Hallo weergave wordt geladen, hello volgende code primes een cache voor onze gebruik.</span><span class="sxs-lookup"><span data-stu-id="8973f-166">Inside `(void)viewDidLoad()`, which is always called after hello view is loaded, hello following code primes a cache for our use.</span></span>

<span data-ttu-id="8973f-167">Hallo na code toevoegen:</span><span class="sxs-lookup"><span data-stu-id="8973f-167">Add hello following code:</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="8973f-168">Maken van een webweergave voor aanmelden</span><span class="sxs-lookup"><span data-stu-id="8973f-168">Create a WebView for sign-in</span></span>
<span data-ttu-id="8973f-169">Een webweergave kunt Hallo gebruiker vragen om aanvullende factoren zoals SMS-bericht (indien geconfigureerd) of fout berichten toohello gebruiker retourneren.</span><span class="sxs-lookup"><span data-stu-id="8973f-169">A WebView can prompt hello user for additional factors like SMS text message (if configured) or return error messages toohello user.</span></span> <span data-ttu-id="8973f-170">Hier moet u instellen Hallo webweergave en later schrijven Hallo code toohandle Hallo retouraanroepen gebeurt in Hallo webweergave van Hallo identity services.</span><span class="sxs-lookup"><span data-stu-id="8973f-170">Here you'll set up hello WebView and then later write hello code toohandle hello callbacks that will happen in hello WebView from hello identity services.</span></span>

```objc
-(void)requestOAuth2Access {
    //toosign in tooMicrosoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate toohello URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-hello-webview-methods-toohandle-authentication"></a><span data-ttu-id="8973f-171">Hallo webweergave methoden toohandle verificatie overschrijven</span><span class="sxs-lookup"><span data-stu-id="8973f-171">Override hello WebView methods toohandle authentication</span></span>
<span data-ttu-id="8973f-172">tootell Hallo webweergave wat er gebeurt wanneer een gebruiker nodig toosign in, zoals eerder besproken, kunt u Hallo na code plakken.</span><span class="sxs-lookup"><span data-stu-id="8973f-172">tootell hello WebView what happens when a user needs toosign in as discussed previously, you can paste hello following code.</span></span>

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get hello auth token from a redirect so we need toohandle that in hello webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // hello webview is where all hello communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if hello UIWebView is showing our authorization URL or consent URL, show hello UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read hello Location from hello UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by hello redirect URL we chose toouse from Microsoft APIs
        //continue hello OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a><span data-ttu-id="8973f-173">Schrijven van code toohandle Hallo resultaat van Hallo OAuth2-aanvraag</span><span class="sxs-lookup"><span data-stu-id="8973f-173">Write code toohandle hello result of hello OAuth2 request</span></span>
<span data-ttu-id="8973f-174">Hallo wordt volgende code afgehandeld Hallo URL omleiding die uit Hallo webweergave retourneert.</span><span class="sxs-lookup"><span data-stu-id="8973f-174">hello following code will handle hello redirectURL that returns from hello WebView.</span></span> <span data-ttu-id="8973f-175">Als verificatie niet geslaagd is, probeert Hallo code het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="8973f-175">If authentication wasn't successful, hello code will try again.</span></span> <span data-ttu-id="8973f-176">Hallo-bibliotheek biedt ondertussen Hallo-fout die u kunt zien in de beheerconsole Hallo of asynchroon verwerkt.</span><span class="sxs-lookup"><span data-stu-id="8973f-176">Meanwhile, hello library will provide hello error that you can see in hello console or handle asynchronously.</span></span>

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse hello response for success or failure
     if (accessResult)
    //if success, complete hello OAuth2 flow by handling hello redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-hello-oauth-context-called-account-store"></a><span data-ttu-id="8973f-177">Hallo OAuth-Context (accountarchief genoemd) instellen</span><span class="sxs-lookup"><span data-stu-id="8973f-177">Set up hello OAuth Context (called account store)</span></span>
<span data-ttu-id="8973f-178">U kunt hier aanroepen `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` op Hallo gedeelde accountarchief voor elke service die u wilt dat Hallo toepassing toobe kunnen tooaccess.</span><span class="sxs-lookup"><span data-stu-id="8973f-178">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on hello shared account store for each service that you want hello application toobe able tooaccess.</span></span> <span data-ttu-id="8973f-179">Hallo-accounttype is een tekenreeks die wordt gebruikt als een id voor een bepaalde service.</span><span class="sxs-lookup"><span data-stu-id="8973f-179">hello account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="8973f-180">Omdat u Hallo Graph API gebruiken, Hallo code verwijst tooit als `"myGraphService"`.</span><span class="sxs-lookup"><span data-stu-id="8973f-180">Because you are accessing hello Graph API, hello code refers tooit as `"myGraphService"`.</span></span> <span data-ttu-id="8973f-181">U instellen een zien die aangeven wanneer iets verandert met Hallo token vervolgens.</span><span class="sxs-lookup"><span data-stu-id="8973f-181">You then set up an observer that will tell you when anything changes with hello token.</span></span> <span data-ttu-id="8973f-182">Nadat u Hallo-token ophalen, u Hallo gebruiker back toohello terug `masterView`.</span><span class="sxs-lookup"><span data-stu-id="8973f-182">After you get hello token, you return hello user back toohello `masterView`.</span></span>

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a><span data-ttu-id="8973f-183">Hallo Master weergave toosearch instellen en gebruikers Hallo van Hallo Graph API weergeven</span><span class="sxs-lookup"><span data-stu-id="8973f-183">Set up hello Master View toosearch and display hello users from hello Graph API</span></span>
<span data-ttu-id="8973f-184">Een model-View-Controller (MVC)-app waarin gegevens worden geretourneerd in raster Hallo Hallo is buiten bereik van deze rondleiding Hallo en veel online zelfstudies wordt uitgelegd hoe toobuild een.</span><span class="sxs-lookup"><span data-stu-id="8973f-184">A Master-View-Controller (MVC) app that displays hello returned data in hello grid is beyond hello scope of this walkthrough, and many online tutorials explain how toobuild one.</span></span> <span data-ttu-id="8973f-185">Alle deze code wordt geraamte Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="8973f-185">All this code is in hello skeleton file.</span></span> <span data-ttu-id="8973f-186">U moet echter wel toodeal met een aantal items in deze MVC-toepassing:</span><span class="sxs-lookup"><span data-stu-id="8973f-186">However, you do need toodeal with a few things in this MVC application:</span></span>

* <span data-ttu-id="8973f-187">Wanneer een gebruiker iets in Hallo zoekveld onderscheppen</span><span class="sxs-lookup"><span data-stu-id="8973f-187">Intercept when a user types something in hello search field</span></span>
* <span data-ttu-id="8973f-188">Geef een object van de gegevens terug toohello MasterView zodat weer te resultaten Hallo in Hallo raster geven</span><span class="sxs-lookup"><span data-stu-id="8973f-188">Provide an object of data back toohello MasterView so it can display hello results in hello grid</span></span>

<span data-ttu-id="8973f-189">We doen die hieronder.</span><span class="sxs-lookup"><span data-stu-id="8973f-189">We'll do those below.</span></span>

### <a name="add-a-check-toosee-if-youre-logged-in"></a><span data-ttu-id="8973f-190">Een selectievakje toosee toevoegen als u bent aangemeld</span><span class="sxs-lookup"><span data-stu-id="8973f-190">Add a check toosee if you're logged in</span></span>
<span data-ttu-id="8973f-191">Hallo toepassing doet weinig als Hallo gebruiker niet is aangemeld, dus is het slimme toocheck als er al een token in Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="8973f-191">hello application does little if hello user is not signed in, so it's smart toocheck if there is already a token in hello cache.</span></span> <span data-ttu-id="8973f-192">Als niet zo is, wordt u omgeleid toohello LoginView voor Hallo gebruiker toosign in.</span><span class="sxs-lookup"><span data-stu-id="8973f-192">If not, you redirect toohello LoginView for hello user toosign in.</span></span> <span data-ttu-id="8973f-193">Als u intrekt, Hallo aanbevolen manier toodo acties wanneer een weergave wordt geladen toouse Hallo is `viewDidLoad()` methode waarmee Apple ons.</span><span class="sxs-lookup"><span data-stu-id="8973f-193">If you recall, hello best way toodo actions when a view loads is toouse hello `viewDidLoad()` method that Apple provides us.</span></span>

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-hello-table-view-when-data-is-received"></a><span data-ttu-id="8973f-194">Hallo tabelweergave bijwerken wanneer gegevens worden ontvangen</span><span class="sxs-lookup"><span data-stu-id="8973f-194">Update hello Table View when data is received</span></span>
<span data-ttu-id="8973f-195">Wanneer Hallo Graph API gegevens retourneert, moet u toodisplay Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="8973f-195">When hello Graph API returns data, you need toodisplay hello data.</span></span> <span data-ttu-id="8973f-196">Voor eenvoud volgt hier alle Hallo tooupdate Hallo codetabel.</span><span class="sxs-lookup"><span data-stu-id="8973f-196">For simplicity, here is all hello code tooupdate hello table.</span></span> <span data-ttu-id="8973f-197">Alleen kunt u de juiste waarden Hallo plakken in uw MVC standaardtekst code.</span><span class="sxs-lookup"><span data-stu-id="8973f-197">You can just paste hello right values in your MVC boilerplate code.</span></span>

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure hello cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a><span data-ttu-id="8973f-198">Geef een manier toocall Hallo Graph API wanneer iemand in het veld van Hallo zoeken typt</span><span class="sxs-lookup"><span data-stu-id="8973f-198">Provide a way toocall hello Graph API when someone types in hello search field</span></span>
<span data-ttu-id="8973f-199">Wanneer een gebruiker typt een zoekopdracht in Hallo vak, hoeft u tooshove die via toohello Graph API.</span><span class="sxs-lookup"><span data-stu-id="8973f-199">When a user types a search in hello box, you need tooshove that over toohello Graph API.</span></span> <span data-ttu-id="8973f-200">Hallo `GraphAPICaller` klasse, die u in de volgende code Hallo bouwt, scheidt Hallo lookup functionaliteit van Hallo presentatie.</span><span class="sxs-lookup"><span data-stu-id="8973f-200">hello `GraphAPICaller` class, which you will build in hello following code, separates hello lookup functionality from hello presentation.</span></span> <span data-ttu-id="8973f-201">Nu gaan we Hallo code schrijven waarmee een zoekopdracht tekens toohello Graph API-feeds.</span><span class="sxs-lookup"><span data-stu-id="8973f-201">For now, let's write hello code that feeds any search characters toohello Graph API.</span></span> <span data-ttu-id="8973f-202">We dit doen door op te geven van een methode met de naam `lookupInGraph`, wat Hallo-tekenreeks die we willen toosearch voor duurt.</span><span class="sxs-lookup"><span data-stu-id="8973f-202">We do this by providing a method called `lookupInGraph`, which takes hello string that we want toosearch for.</span></span>

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a><span data-ttu-id="8973f-203">Schrijven van een Helper-klasse tooaccess Hallo Graph API</span><span class="sxs-lookup"><span data-stu-id="8973f-203">Write a Helper class tooaccess hello Graph API</span></span>
<span data-ttu-id="8973f-204">Dit is Hallo kern van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="8973f-204">This is hello core of our application.</span></span> <span data-ttu-id="8973f-205">Hallo rest is code invoegen in Hallo standaardpatroon MVC bij Apple, hier maar geschreven code tooquery Hallo grafiek terwijl Hallo gebruiker typen en vervolgens deze gegevens worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="8973f-205">Whereas hello rest was inserting code in hello default MVC pattern from Apple, here you write code tooquery hello graph as hello user types and then return that data.</span></span> <span data-ttu-id="8973f-206">Hier is Hallo code en een gedetailleerde uitleg erop volgt.</span><span class="sxs-lookup"><span data-stu-id="8973f-206">Here's hello code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="8973f-207">Maak een nieuw Objective C-header-bestand</span><span class="sxs-lookup"><span data-stu-id="8973f-207">Create a new Objective C header file</span></span>
<span data-ttu-id="8973f-208">Bestand met de Hallo `GraphAPICaller.h`, en Hallo volgende code toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="8973f-208">Name hello file `GraphAPICaller.h`, and add hello following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="8973f-209">Hier ziet u dat een opgegeven methode een tekenreeks zijn wordt en een completionBlock retourneert.</span><span class="sxs-lookup"><span data-stu-id="8973f-209">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="8973f-210">Deze completionBlock wordt als u mogelijk hebt geraden, bijgewerkt Hallo tabel verstrekken die een object met ingevulde gegevens in realtime Hallo gebruikers zoeken.</span><span class="sxs-lookup"><span data-stu-id="8973f-210">This completionBlock, as you may have guessed, will update hello table by providing an object with populated data in real time as hello user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="8973f-211">Maak een nieuw Objective C-bestand</span><span class="sxs-lookup"><span data-stu-id="8973f-211">Create a new Objective C file</span></span>
<span data-ttu-id="8973f-212">Bestand met de Hallo `GraphAPICaller.m`, en Hallo volgende methode toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="8973f-212">Name hello file `GraphAPICaller.m`, and add hello following method.</span></span>

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
                           }

                           completionBlock(Users, nil);
                       }
                       else
                       {
                           completionBlock(nil, error);
                       }

                   }];
}

```

<span data-ttu-id="8973f-213">We gaan met deze methode in detail.</span><span class="sxs-lookup"><span data-stu-id="8973f-213">Let's go through this method in detail.</span></span>

<span data-ttu-id="8973f-214">Hallo-kern van deze code is in Hallo `NXOAuth2Request`, methode waarmee de Hallo parameters zijn vereist die u al hebt gedefinieerd in Hallo settings.plist-bestand.</span><span class="sxs-lookup"><span data-stu-id="8973f-214">hello core of this code is in hello `NXOAuth2Request`, method which takes hello parameters that you've already defined in hello settings.plist file.</span></span>

<span data-ttu-id="8973f-215">de eerste stap Hallo is tooconstruct Hallo rechts Graph API-aanroep.</span><span class="sxs-lookup"><span data-stu-id="8973f-215">hello first step is tooconstruct hello right Graph API call.</span></span> <span data-ttu-id="8973f-216">Omdat u aanroept `/users`, u opgeven dat door deze toohello Graph API resource samen met de Hallo-versie toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="8973f-216">Because you are calling `/users`, you specify that by appending it toohello Graph API resource along with hello version.</span></span> <span data-ttu-id="8973f-217">Het maakt zin tooput deze in een bestand met externe instellingen omdat deze wijzigen kunnen, zoals Hallo API ontwikkeld.</span><span class="sxs-lookup"><span data-stu-id="8973f-217">It makes sense tooput these in an external settings file because these can change as hello API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="8973f-218">Vervolgens moet u toospecify parameters dat u ook toohello Graph API-aanroep bieden.</span><span class="sxs-lookup"><span data-stu-id="8973f-218">Next, you need toospecify parameters that you will also provide toohello Graph API call.</span></span> <span data-ttu-id="8973f-219">Het is *erg belangrijk* plaats Hallo-parameters niet in de resource-eindpunt Hallo omdat die is verwijderd voor alle niet-URI die voldoen tekens tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="8973f-219">It is *very important* that you do not put hello parameters in hello resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="8973f-220">Alle querycode moet worden opgegeven in het Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="8973f-220">All query code must be provided in hello parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="8973f-221">U wellicht opgevallen dat hiermee een `convertParamsToDictionary` methode die u nog niet hebt geschreven.</span><span class="sxs-lookup"><span data-stu-id="8973f-221">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="8973f-222">Laten we dit nu doen aan Hallo einde van Hallo-bestand:</span><span class="sxs-lookup"><span data-stu-id="8973f-222">Let's do so now at hello end of hello file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="8973f-223">Vervolgens gebruiken we Hallo `NXOAuth2Request` methode tooget gegevens weer van Hallo API in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="8973f-223">Next, let's use hello `NXOAuth2Request` method tooget data back from hello API in JSON format.</span></span>

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

<span data-ttu-id="8973f-224">Ten slotte bekijken we hoe u Hallo gegevens toohello MasterViewController retourneren.</span><span class="sxs-lookup"><span data-stu-id="8973f-224">Finally, let's look at how you return hello data toohello MasterViewController.</span></span> <span data-ttu-id="8973f-225">Hallo gegevens retourneert als geserialiseerd en toobe gedeserialiseerd moet en geladen in een object dat Hallo MainViewController kan gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8973f-225">hello data returns as serialized and needs toobe deserialized and loaded in an object that hello MainViewController can consume.</span></span> <span data-ttu-id="8973f-226">Voor dit doel Hallo basisproject heeft een `User.m/h` -bestand dat wordt gemaakt van een gebruikersobject.</span><span class="sxs-lookup"><span data-stu-id="8973f-226">For this purpose, hello skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="8973f-227">U vullen dat object gebruiker met informatie uit Hallo grafiek.</span><span class="sxs-lookup"><span data-stu-id="8973f-227">You populate that User object with information from hello graph.</span></span>

```objc
                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-hello-sample"></a><span data-ttu-id="8973f-228">Hallo-voorbeeld uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8973f-228">Run hello sample</span></span>
<span data-ttu-id="8973f-229">Als u hebt gebruikt Hallo basisproject of gevolgd samen met de Hallo scenario moet nu uw toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8973f-229">If you've used hello skeleton or followed along with hello walkthrough your application should now run.</span></span> <span data-ttu-id="8973f-230">Hallo simulator Start en op **aanmelden** toouse Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="8973f-230">Start hello simulator and click **Sign in** toouse hello application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="8973f-231">Beveiligingsupdates voor onze product</span><span class="sxs-lookup"><span data-stu-id="8973f-231">Get security updates for our product</span></span>
<span data-ttu-id="8973f-232">We raden u tooget meldingen van wanneer er beveiligingsincidenten optreden door te bezoeken Hallo [Security TechCenter](https://technet.microsoft.com/security/dd252948) en u te abonneren tooSecurity Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="8973f-232">We encourage you tooget notifications of when security incidents occur by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

