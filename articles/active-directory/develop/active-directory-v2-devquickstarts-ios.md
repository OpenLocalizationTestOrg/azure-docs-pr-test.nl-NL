---
title: Aanmelden toevoegen aan een iOS-toepassing met behulp van het Azure AD v2.0-eindpunt | Microsoft Docs
description: Het bouwen van een iOS-app die gebruikers met beide persoonlijke Microsoft-account aanmeldt en werk- of schoolaccount accounts met behulp van de bibliotheken van derden.
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
ms.openlocfilehash: cf1455dc3d55ea3581195f7a315556d134c23a26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-ios-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="92a82-103">Aanmelden voor een iOS-app met behulp van een derde partij-bibliotheek met Graph API met behulp van het v2.0-eindpunt toevoegen</span><span class="sxs-lookup"><span data-stu-id="92a82-103">Add sign-in to an iOS app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="92a82-104">Op het Microsoft Identity-platform wordt gebruikgemaakt van open standaarden, zoals OAuth2 en OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="92a82-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="92a82-105">Ontwikkelaars kunnen een bibliotheek die ze willen integreren in onze services gebruiken.</span><span class="sxs-lookup"><span data-stu-id="92a82-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="92a82-106">Om te helpen ons platform gebruiken met andere bibliotheken ontwikkelaars, hebben we enkele scenario's zoals deze voorbeelden van het configureren van derden bibliotheken verbinding maken met het identiteitsplatform van Microsoft geschreven.</span><span class="sxs-lookup"><span data-stu-id="92a82-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="92a82-107">De meeste bibliotheken die implementeren [de RFC6749 OAuth2-specificatie](https://tools.ietf.org/html/rfc6749) verbinding kunnen maken met het identiteitsplatform van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="92a82-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="92a82-108">Met de toepassing die in dit scenario maakt, kunnen gebruikers zich aanmelden bij hun organisatie en zoekt u naar anderen binnen hun organisatie met behulp van de Graph API.</span><span class="sxs-lookup"><span data-stu-id="92a82-108">With the application that this walkthrough creates, users can sign in to their organization and then search for others in their organization by using the Graph API.</span></span>

<span data-ttu-id="92a82-109">Als u geen ervaring met OAuth2 of OpenID Connect, wellicht veel van de configuratie van deze niet verstandig aan u.</span><span class="sxs-lookup"><span data-stu-id="92a82-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="92a82-110">Het is raadzaam dat u leest [v2.0-protocollen - stromen van OAuth 2.0 autorisatie Code](active-directory-v2-protocols-oauth-code.md) voor de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="92a82-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="92a82-111">Sommige functies van ons platform die u een expressie in de OAuth2 of OpenID Connect standaarden, zoals voorwaardelijke toegang en beheer van Intune-beleid hebt, moeten u onze open-source bibliotheken voor Microsoft Azure identiteit gebruiken.</span><span class="sxs-lookup"><span data-stu-id="92a82-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="92a82-112">Het v2.0-eindpunt biedt geen ondersteuning voor alle Azure Active Directory-scenario's en onderdelen.</span><span class="sxs-lookup"><span data-stu-id="92a82-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="92a82-113">Meer informatie over om te bepalen of moet u het v2.0-eindpunt, [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="92a82-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="92a82-114">Code vanuit GitHub downloaden</span><span class="sxs-lookup"><span data-stu-id="92a82-114">Download code from GitHub</span></span>
<span data-ttu-id="92a82-115">De code voor deze zelfstudie wordt onderhouden in [GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span><span class="sxs-lookup"><span data-stu-id="92a82-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="92a82-116">Als u wilt volgen, kunt u [basis van de app downloaden als een ZIP-](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) of het geraamte:</span><span class="sxs-lookup"><span data-stu-id="92a82-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="92a82-117">U kunt ook het voorbeeld downloaden en meteen aan de slag:</span><span class="sxs-lookup"><span data-stu-id="92a82-117">You can also just download the sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="92a82-118">Een app registreren</span><span class="sxs-lookup"><span data-stu-id="92a82-118">Register an app</span></span>
<span data-ttu-id="92a82-119">Maakt een nieuwe app op de [toepassing registratieportal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of de gedetailleerde stappen op [het registreren van een app met het v2.0-eindpunt](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="92a82-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at  [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="92a82-120">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="92a82-120">Make sure to:</span></span>

* <span data-ttu-id="92a82-121">Kopieer de **toepassings-Id** die toegewezen aan uw app, omdat u hebt deze snel nodig.</span><span class="sxs-lookup"><span data-stu-id="92a82-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="92a82-122">Voeg de **Mobile** platform voor uw app.</span><span class="sxs-lookup"><span data-stu-id="92a82-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="92a82-123">Kopieer de **omleidings-URI** vanuit de portal.</span><span class="sxs-lookup"><span data-stu-id="92a82-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="92a82-124">Moet u de standaardwaarde van `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="92a82-124">You must use the default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-the-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="92a82-125">De derde partij NXOAuth2 bibliotheek downloaden en een werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="92a82-125">Download the third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="92a82-126">Voor dit scenario moet u de OAuth2Client vanuit GitHub, namelijk een OAuth2-bibliotheek voor Mac OS X- en iOS (Cocoa en Cocoa touch) gebruikt.</span><span class="sxs-lookup"><span data-stu-id="92a82-126">For this walkthrough, you will use the OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="92a82-127">Deze bibliotheek is gebaseerd op concept 10 van de OAuth2-specificatie.</span><span class="sxs-lookup"><span data-stu-id="92a82-127">This library is based on draft 10 of the OAuth2 spec.</span></span> <span data-ttu-id="92a82-128">Het systeemeigen toepassingsprofiel implementeert en biedt ondersteuning voor het eindpunt voor autorisatie van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="92a82-128">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="92a82-129">Dit zijn alle dingen die u wilt integreren met het identiteitsplatform van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="92a82-129">These are all the things you'll need to integrate with the Microsoft identity platform.</span></span>

### <a name="add-the-library-to-your-project-by-using-cocoapods"></a><span data-ttu-id="92a82-130">De bibliotheek toevoegen aan uw project via CocoaPods</span><span class="sxs-lookup"><span data-stu-id="92a82-130">Add the library to your project by using CocoaPods</span></span>
<span data-ttu-id="92a82-131">CocoaPods is een hulpmiddel voor afhankelijkheidsbeheer voor Xcode-projecten.</span><span class="sxs-lookup"><span data-stu-id="92a82-131">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="92a82-132">Hiermee worden de vorige installatiestappen automatisch beheerd.</span><span class="sxs-lookup"><span data-stu-id="92a82-132">It manages the previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="92a82-133">Voeg het volgende aan de podfile toe:</span><span class="sxs-lookup"><span data-stu-id="92a82-133">Add the following to this podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="92a82-134">De podfile laden via CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="92a82-134">Load the podfile by using CocoaPods.</span></span> <span data-ttu-id="92a82-135">Hiermee maakt u een nieuwe Xcode-werkruimte die u gaat laden.</span><span class="sxs-lookup"><span data-stu-id="92a82-135">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-the-structure-of-the-project"></a><span data-ttu-id="92a82-136">De structuur van het project verkennen</span><span class="sxs-lookup"><span data-stu-id="92a82-136">Explore the structure of the project</span></span>
<span data-ttu-id="92a82-137">De volgende structuur is ingesteld voor het project in het geraamte opgenomen:</span><span class="sxs-lookup"><span data-stu-id="92a82-137">The following structure is set up for our project in the skeleton:</span></span>

* <span data-ttu-id="92a82-138">Een Master-weergave met een zoekopdracht UPN</span><span class="sxs-lookup"><span data-stu-id="92a82-138">A Master View with a UPN Search</span></span>
* <span data-ttu-id="92a82-139">Een detailweergave voor de gegevens over de geselecteerde gebruiker</span><span class="sxs-lookup"><span data-stu-id="92a82-139">A Detail View for the data about the selected user</span></span>
* <span data-ttu-id="92a82-140">Een aanmelding weergave waar een gebruiker bij de app aanmelden zich om op te vragen van de grafiek</span><span class="sxs-lookup"><span data-stu-id="92a82-140">A Login View where a user can sign in to the app to query the graph</span></span>

<span data-ttu-id="92a82-141">Er wordt verplaatst naar verschillende bestanden in de basis voor verificatie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="92a82-141">We will move to various files in the skeleton to add authentication.</span></span> <span data-ttu-id="92a82-142">Andere onderdelen van de code, zoals de visual code, niet van toepassing zijn op identiteit, maar zijn beschikbaar voor u.</span><span class="sxs-lookup"><span data-stu-id="92a82-142">Other parts of the code, such as the visual code, do not pertain to identity but are provided for you.</span></span>

## <a name="set-up-the-settingsplst-file-in-the-library"></a><span data-ttu-id="92a82-143">Instellen van het bestand settings.plst in de bibliotheek</span><span class="sxs-lookup"><span data-stu-id="92a82-143">Set up the settings.plst file in the library</span></span>
* <span data-ttu-id="92a82-144">Open in de Quick Start-project het `settings.plist` bestand.</span><span class="sxs-lookup"><span data-stu-id="92a82-144">In the QuickStart project, open the `settings.plist` file.</span></span> <span data-ttu-id="92a82-145">Vervang de waarden van de elementen in de sectie in overeenstemming met de waarden die u in de Azure portal gebruikt.</span><span class="sxs-lookup"><span data-stu-id="92a82-145">Replace the values of the elements in the section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="92a82-146">Uw code verwijst naar deze waarden als de Active Directory Authentication Library wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="92a82-146">Your code will reference these values whenever it uses the Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="92a82-147">De `clientId` is de client-ID van uw toepassing die u hebt gekopieerd uit de portal.</span><span class="sxs-lookup"><span data-stu-id="92a82-147">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="92a82-148">De `redirectUri` is de omleidings-URL die de portal worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="92a82-148">The `redirectUri` is the redirect URL that the portal provided.</span></span>

## <a name="set-up-the-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="92a82-149">De bibliotheek NXOAuth2Client in uw LoginViewController instellen</span><span class="sxs-lookup"><span data-stu-id="92a82-149">Set up the NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="92a82-150">De bibliotheek NXOAuth2Client moet sommige waarden ophalen instellen.</span><span class="sxs-lookup"><span data-stu-id="92a82-150">The NXOAuth2Client library requires some values to get set up.</span></span> <span data-ttu-id="92a82-151">Nadat u die taak hebt voltooid, kunt u het verkregen token de Graph-API aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="92a82-151">After you complete that task, you can use the acquired token to call the Graph API.</span></span> <span data-ttu-id="92a82-152">Omdat `LoginView` wordt aangeroepen op elk gewenst moment moeten we verifiëren, is het verstandig om configuratiewaarden in aan dat bestand.</span><span class="sxs-lookup"><span data-stu-id="92a82-152">Because `LoginView` will be called any time we need to authenticate, it makes sense to put configuration values in to that file.</span></span>

* <span data-ttu-id="92a82-153">Laten we enkele Voeg waarden toe aan de `LoginViewController.m` bestand in te stellen de context voor verificatie en autorisatie.</span><span class="sxs-lookup"><span data-stu-id="92a82-153">Let's add some values to the  `LoginViewController.m` file to set the context for authentication and authorization.</span></span> <span data-ttu-id="92a82-154">Meer informatie over de waarden volgt u de code.</span><span class="sxs-lookup"><span data-stu-id="92a82-154">Details about the values follow the code.</span></span>
  
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

<span data-ttu-id="92a82-155">Bekijk meer informatie over de code in.</span><span class="sxs-lookup"><span data-stu-id="92a82-155">Let's look at details about the code.</span></span>

<span data-ttu-id="92a82-156">De eerste tekenreeks is voor `scopes`.</span><span class="sxs-lookup"><span data-stu-id="92a82-156">The first string is for `scopes`.</span></span>  <span data-ttu-id="92a82-157">De `User.Read` waarde kunt u lezen van het profiel van de basis van de aangemelde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="92a82-157">The `User.Read` value allows you to read the basic profile of the signed in user.</span></span>

<span data-ttu-id="92a82-158">U kunt meer informatie over de beschikbare scopes op [Microsoft Graph-machtigingsbereiken](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="92a82-158">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="92a82-159">Voor `authURL`, `loginURL`, `bhh`, en `tokenURL`, moet u de waarden die eerder is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="92a82-159">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use the values provided previously.</span></span> <span data-ttu-id="92a82-160">Als u de open-source bibliotheken voor Microsoft Azure identiteit gebruikt, halen we deze gegevens voor u met behulp van onze metagegevenseindpunt.</span><span class="sxs-lookup"><span data-stu-id="92a82-160">If you use the open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="92a82-161">Deze waarden zijn al voor u uitgepakt.</span><span class="sxs-lookup"><span data-stu-id="92a82-161">We've done the hard work of extracting these values for you.</span></span>

<span data-ttu-id="92a82-162">De waarde `keychain` is de container die de bibliotheek NXOAuth2Client gebruikt voor het maken van een sleutelhanger waarin uw tokens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="92a82-162">The `keychain` value is the container that the NXOAuth2Client library will use to create a keychain to store your tokens.</span></span> <span data-ttu-id="92a82-163">Als u wilt ophalen van eenmalige aanmelding (SSO) via talrijke apps, kunt u de dezelfde sleutelketen opgeven in elk van uw toepassingen en aanvragen van het gebruik van die sleutelhanger in uw Xcode-rechten.</span><span class="sxs-lookup"><span data-stu-id="92a82-163">If you'd like to get single sign-on (SSO) across numerous apps, you can specify the same keychain in each of your applications and request the use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="92a82-164">Dit wordt uitgelegd in de Apple-documentatie.</span><span class="sxs-lookup"><span data-stu-id="92a82-164">This is explained in the Apple documentation.</span></span>

<span data-ttu-id="92a82-165">De rest van deze waarden zijn vereist voor de bibliotheek gebruiken en maken van de plaatsen waar u bij het uitvoeren van de waarden voor de context.</span><span class="sxs-lookup"><span data-stu-id="92a82-165">The rest of these values are required to use the library and create places for you to carry values to the context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="92a82-166">Een URL-cache maken</span><span class="sxs-lookup"><span data-stu-id="92a82-166">Create a URL cache</span></span>
<span data-ttu-id="92a82-167">Binnen `(void)viewDidLoad()`, die altijd wordt aangeroepen nadat de weergave wordt geladen, de volgende code primes een cache voor onze gebruik.</span><span class="sxs-lookup"><span data-stu-id="92a82-167">Inside `(void)viewDidLoad()`, which is always called after the view is loaded, the following code primes a cache for our use.</span></span>

<span data-ttu-id="92a82-168">Voeg de volgende code toe:</span><span class="sxs-lookup"><span data-stu-id="92a82-168">Add the following code:</span></span>

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

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="92a82-169">Maken van een webweergave voor aanmelden</span><span class="sxs-lookup"><span data-stu-id="92a82-169">Create a WebView for sign-in</span></span>
<span data-ttu-id="92a82-170">Een webweergave kan de gebruiker gevraagd om aanvullende factoren zoals SMS-bericht (indien geconfigureerd) of foutberichten terug naar de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="92a82-170">A WebView can prompt the user for additional factors like SMS text message (if configured) or return error messages to the user.</span></span> <span data-ttu-id="92a82-171">Hier stelt u de webweergave boven en vervolgens de code voor het afhandelen van de retouraanroepen die in de webweergave van de services identiteit gebeurt later te schrijven.</span><span class="sxs-lookup"><span data-stu-id="92a82-171">Here you'll set up the WebView and then later write the code to handle the callbacks that will happen in the WebView from the identity services.</span></span>

```objc
-(void)requestOAuth2Access {
    //to sign in to Microsoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate to the URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-the-webview-methods-to-handle-authentication"></a><span data-ttu-id="92a82-172">De WebView-methoden voor het afhandelen van verificatie overschrijven</span><span class="sxs-lookup"><span data-stu-id="92a82-172">Override the WebView methods to handle authentication</span></span>
<span data-ttu-id="92a82-173">Om te laten de webweergave wat er gebeurt wanneer een gebruiker aanmelden moet, zoals eerder besproken, kunt u de volgende code plakken.</span><span class="sxs-lookup"><span data-stu-id="92a82-173">To tell the WebView what happens when a user needs to sign in as discussed previously, you can paste the following code.</span></span>

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get the auth token from a redirect so we need to handle that in the webview.

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

    // The webview is where all the communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if the UIWebView is showing our authorization URL or consent URL, show the UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide the UIWebView, we've left the authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read the Location from the UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by the redirect URL we chose to use from Microsoft APIs
        //continue the OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-to-handle-the-result-of-the-oauth2-request"></a><span data-ttu-id="92a82-174">Code schrijven om het resultaat van de OAuth2-aanvraag af te handelen</span><span class="sxs-lookup"><span data-stu-id="92a82-174">Write code to handle the result of the OAuth2 request</span></span>
<span data-ttu-id="92a82-175">De volgende code wordt de URL van de omleiding die als resultaat de webweergave geeft afgehandeld.</span><span class="sxs-lookup"><span data-stu-id="92a82-175">The following code will handle the redirectURL that returns from the WebView.</span></span> <span data-ttu-id="92a82-176">Als verificatie niet geslaagd is, probeert de code het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="92a82-176">If authentication wasn't successful, the code will try again.</span></span> <span data-ttu-id="92a82-177">De fout die u kunt zien in de beheerconsole of asynchroon verwerken krijgt ondertussen van de bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="92a82-177">Meanwhile, the library will provide the error that you can see in the console or handle asynchronously.</span></span>

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse the response for success or failure
     if (accessResult)
    //if success, complete the OAuth2 flow by handling the redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-the-oauth-context-called-account-store"></a><span data-ttu-id="92a82-178">Instellen van de OAuth-Context (accountarchief genoemd)</span><span class="sxs-lookup"><span data-stu-id="92a82-178">Set up the OAuth Context (called account store)</span></span>
<span data-ttu-id="92a82-179">U kunt hier aanroepen `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` op de gedeelde accountarchief voor elke service die u wilt toegang krijgen tot de toepassing.</span><span class="sxs-lookup"><span data-stu-id="92a82-179">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on the shared account store for each service that you want the application to be able to access.</span></span> <span data-ttu-id="92a82-180">Het accounttype is een tekenreeks die wordt gebruikt als een id voor een bepaalde service.</span><span class="sxs-lookup"><span data-stu-id="92a82-180">The account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="92a82-181">Omdat u de Graph API opent, wordt de code verwijst naar als `"myGraphService"`.</span><span class="sxs-lookup"><span data-stu-id="92a82-181">Because you are accessing the Graph API, the code refers to it as `"myGraphService"`.</span></span> <span data-ttu-id="92a82-182">U instellen een zien die aangeven wanneer iets verandert met het token vervolgens.</span><span class="sxs-lookup"><span data-stu-id="92a82-182">You then set up an observer that will tell you when anything changes with the token.</span></span> <span data-ttu-id="92a82-183">Nadat u het token, u terugkeert de gebruiker terug naar de `masterView`.</span><span class="sxs-lookup"><span data-stu-id="92a82-183">After you get the token, you return the user back to the `masterView`.</span></span>

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

## <a name="set-up-the-master-view-to-search-and-display-the-users-from-the-graph-api"></a><span data-ttu-id="92a82-184">Instellen van de Master-weergave te zoeken en weer van de gebruikers van de Graph API</span><span class="sxs-lookup"><span data-stu-id="92a82-184">Set up the Master View to search and display the users from the Graph API</span></span>
<span data-ttu-id="92a82-185">Een model-View-Controller (MVC)-app die wordt weergegeven van de geretourneerde gegevens in het raster is buiten het bereik van dit scenario en veel online zelfstudies wordt uitgelegd hoe u een bouwen.</span><span class="sxs-lookup"><span data-stu-id="92a82-185">A Master-View-Controller (MVC) app that displays the returned data in the grid is beyond the scope of this walkthrough, and many online tutorials explain how to build one.</span></span> <span data-ttu-id="92a82-186">Alle deze code is in het geraamte bestand.</span><span class="sxs-lookup"><span data-stu-id="92a82-186">All this code is in the skeleton file.</span></span> <span data-ttu-id="92a82-187">U moet echter te maken met een aantal items in deze MVC-toepassing:</span><span class="sxs-lookup"><span data-stu-id="92a82-187">However, you do need to deal with a few things in this MVC application:</span></span>

* <span data-ttu-id="92a82-188">Wanneer een gebruiker iets in het zoekveld onderscheppen</span><span class="sxs-lookup"><span data-stu-id="92a82-188">Intercept when a user types something in the search field</span></span>
* <span data-ttu-id="92a82-189">Een object van de gegevens terug naar de MasterView bieden, zodat de resultaten kan worden weergegeven in het raster</span><span class="sxs-lookup"><span data-stu-id="92a82-189">Provide an object of data back to the MasterView so it can display the results in the grid</span></span>

<span data-ttu-id="92a82-190">We doen die hieronder.</span><span class="sxs-lookup"><span data-stu-id="92a82-190">We'll do those below.</span></span>

### <a name="add-a-check-to-see-if-youre-logged-in"></a><span data-ttu-id="92a82-191">Toevoegen van een selectievakje om te zien als u bent aangemeld</span><span class="sxs-lookup"><span data-stu-id="92a82-191">Add a check to see if you're logged in</span></span>
<span data-ttu-id="92a82-192">De toepassing biedt weinig als de gebruiker niet is ondertekend, dus is het verstandig om te controleren of er al een token in de cache.</span><span class="sxs-lookup"><span data-stu-id="92a82-192">The application does little if the user is not signed in, so it's smart to check if there is already a token in the cache.</span></span> <span data-ttu-id="92a82-193">Als dat niet het geval is, wordt u omgeleid naar de LoginView voor de gebruiker aan te melden.</span><span class="sxs-lookup"><span data-stu-id="92a82-193">If not, you redirect to the LoginView for the user to sign in.</span></span> <span data-ttu-id="92a82-194">Als u intrekt, wordt de beste manier acties uitvoeren wanneer een weergave wordt geladen is met de `viewDidLoad()` methode waarmee Apple ons.</span><span class="sxs-lookup"><span data-stu-id="92a82-194">If you recall, the best way to do actions when a view loads is to use the `viewDidLoad()` method that Apple provides us.</span></span>

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

### <a name="update-the-table-view-when-data-is-received"></a><span data-ttu-id="92a82-195">De weergave van de tabel niet bijwerken wanneer gegevens worden ontvangen</span><span class="sxs-lookup"><span data-stu-id="92a82-195">Update the Table View when data is received</span></span>
<span data-ttu-id="92a82-196">Wanneer de Graph API gegevens retourneert, moet u de gegevens worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="92a82-196">When the Graph API returns data, you need to display the data.</span></span> <span data-ttu-id="92a82-197">Voor eenvoud, moet u hier de code voor het bijwerken van de tabel is.</span><span class="sxs-lookup"><span data-stu-id="92a82-197">For simplicity, here is all the code to update the table.</span></span> <span data-ttu-id="92a82-198">U kunt alleen de juiste waarden in uw MVC standaardtekst code plakken.</span><span class="sxs-lookup"><span data-stu-id="92a82-198">You can just paste the right values in your MVC boilerplate code.</span></span>

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


    // Configure the cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-to-call-the-graph-api-when-someone-types-in-the-search-field"></a><span data-ttu-id="92a82-199">Bieden een manier om de Graph API aanroepen wanneer iemand in het zoekveld typt</span><span class="sxs-lookup"><span data-stu-id="92a82-199">Provide a way to call the Graph API when someone types in the search field</span></span>
<span data-ttu-id="92a82-200">Wanneer een gebruiker typt een zoekopdracht in het vak, moet u die via shove voor Graph API.</span><span class="sxs-lookup"><span data-stu-id="92a82-200">When a user types a search in the box, you need to shove that over to the Graph API.</span></span> <span data-ttu-id="92a82-201">De `GraphAPICaller` klasse, die u in de volgende code bouwt, scheidt u de lookup-functionaliteit van de presentatie.</span><span class="sxs-lookup"><span data-stu-id="92a82-201">The `GraphAPICaller` class, which you will build in the following code, separates the lookup functionality from the presentation.</span></span> <span data-ttu-id="92a82-202">Nu gaan we de code schrijven waarmee willekeurige tekens search-feeds voor Graph API.</span><span class="sxs-lookup"><span data-stu-id="92a82-202">For now, let's write the code that feeds any search characters to the Graph API.</span></span> <span data-ttu-id="92a82-203">We dit doen door op te geven van een methode met de naam `lookupInGraph`, wat de tekenreeks die u zoeken wilt naar duurt.</span><span class="sxs-lookup"><span data-stu-id="92a82-203">We do this by providing a method called `lookupInGraph`, which takes the string that we want to search for.</span></span>

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

## <a name="write-a-helper-class-to-access-the-graph-api"></a><span data-ttu-id="92a82-204">Schrijven van een helperklasse voor toegang tot de Graph API</span><span class="sxs-lookup"><span data-stu-id="92a82-204">Write a Helper class to access the Graph API</span></span>
<span data-ttu-id="92a82-205">Dit is de kern van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="92a82-205">This is the core of our application.</span></span> <span data-ttu-id="92a82-206">Terwijl de rest code in het standaard MVC bij Apple invoegen is, schrijven hier u code voor de grafiek niet opvragen als het gebruikerstypen en ga daarna terug die gegevens.</span><span class="sxs-lookup"><span data-stu-id="92a82-206">Whereas the rest was inserting code in the default MVC pattern from Apple, here you write code to query the graph as the user types and then return that data.</span></span> <span data-ttu-id="92a82-207">Dit is de code en een gedetailleerde uitleg erop volgt.</span><span class="sxs-lookup"><span data-stu-id="92a82-207">Here's the code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="92a82-208">Maak een nieuw Objective C-header-bestand</span><span class="sxs-lookup"><span data-stu-id="92a82-208">Create a new Objective C header file</span></span>
<span data-ttu-id="92a82-209">Noem het bestand `GraphAPICaller.h`, en voeg de volgende code.</span><span class="sxs-lookup"><span data-stu-id="92a82-209">Name the file `GraphAPICaller.h`, and add the following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="92a82-210">Hier ziet u dat een opgegeven methode een tekenreeks zijn wordt en een completionBlock retourneert.</span><span class="sxs-lookup"><span data-stu-id="92a82-210">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="92a82-211">Deze completionBlock omdat u mogelijk hebt geraden, wordt de tabel bijwerken door te geven van een object met ingevulde gegevens in realtime als de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="92a82-211">This completionBlock, as you may have guessed, will update the table by providing an object with populated data in real time as the user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="92a82-212">Maak een nieuw Objective C-bestand</span><span class="sxs-lookup"><span data-stu-id="92a82-212">Create a new Objective C file</span></span>
<span data-ttu-id="92a82-213">Noem het bestand `GraphAPICaller.m`, en voeg de volgende methode toe.</span><span class="sxs-lookup"><span data-stu-id="92a82-213">Name the file `GraphAPICaller.m`, and add the following method.</span></span>

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
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
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

<span data-ttu-id="92a82-214">We gaan met deze methode in detail.</span><span class="sxs-lookup"><span data-stu-id="92a82-214">Let's go through this method in detail.</span></span>

<span data-ttu-id="92a82-215">De kern van deze code is in de `NXOAuth2Request`, methode waarmee de parameters die u al hebt gedefinieerd in het bestand settings.plist.</span><span class="sxs-lookup"><span data-stu-id="92a82-215">The core of this code is in the `NXOAuth2Request`, method which takes the parameters that you've already defined in the settings.plist file.</span></span>

<span data-ttu-id="92a82-216">De eerste stap is om de juiste Graph API-aanroep samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="92a82-216">The first step is to construct the right Graph API call.</span></span> <span data-ttu-id="92a82-217">Omdat u aanroept `/users`, u opgeven dat door deze te voegen aan de resource Graph API samen met de versie.</span><span class="sxs-lookup"><span data-stu-id="92a82-217">Because you are calling `/users`, you specify that by appending it to the Graph API resource along with the version.</span></span> <span data-ttu-id="92a82-218">Het zinvol om deze in een bestand met externe instellingen omdat deze wijzigen kunnen, zoals de API ontwikkeld.</span><span class="sxs-lookup"><span data-stu-id="92a82-218">It makes sense to put these in an external settings file because these can change as the API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="92a82-219">Vervolgens moet u parameters opgeven die u ook voor de Graph API-aanroep biedt.</span><span class="sxs-lookup"><span data-stu-id="92a82-219">Next, you need to specify parameters that you will also provide to the Graph API call.</span></span> <span data-ttu-id="92a82-220">Het is *erg belangrijk* plaats de parameters niet in het resource-eindpunt omdat die is verwijderd voor alle niet-URI die voldoen tekens tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="92a82-220">It is *very important* that you do not put the parameters in the resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="92a82-221">Alle querycode moet worden opgegeven in de parameters.</span><span class="sxs-lookup"><span data-stu-id="92a82-221">All query code must be provided in the parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="92a82-222">U wellicht opgevallen dat hiermee een `convertParamsToDictionary` methode die u nog niet hebt geschreven.</span><span class="sxs-lookup"><span data-stu-id="92a82-222">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="92a82-223">Laten we dit nu doen aan het einde van het bestand:</span><span class="sxs-lookup"><span data-stu-id="92a82-223">Let's do so now at the end of the file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="92a82-224">Vervolgens gebruiken we de `NXOAuth2Request` methode terug gegevens ophalen van de API in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="92a82-224">Next, let's use the `NXOAuth2Request` method to get data back from the API in JSON format.</span></span>

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
                       // Process the response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

<span data-ttu-id="92a82-225">Tot slot gaan we kijken hoe u de gegevens terug naar de MasterViewController.</span><span class="sxs-lookup"><span data-stu-id="92a82-225">Finally, let's look at how you return the data to the MasterViewController.</span></span> <span data-ttu-id="92a82-226">De gegevens retourneert als geserialiseerd en moet worden gedeserialiseerd en geladen in een object dat de MainViewController kan gebruiken.</span><span class="sxs-lookup"><span data-stu-id="92a82-226">The data returns as serialized and needs to be deserialized and loaded in an object that the MainViewController can consume.</span></span> <span data-ttu-id="92a82-227">Voor dit doel het basisproject heeft een `User.m/h` -bestand dat wordt gemaakt van een gebruikersobject.</span><span class="sxs-lookup"><span data-stu-id="92a82-227">For this purpose, the skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="92a82-228">Vullen van dat object gebruiker met informatie van de grafiek.</span><span class="sxs-lookup"><span data-stu-id="92a82-228">You populate that User object with information from the graph.</span></span>

```objc
                           // We can grab the top most JSON node to get our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by the key name being "value". It really is the name of the
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


## <a name="run-the-sample"></a><span data-ttu-id="92a82-229">Het voorbeeld uitvoert</span><span class="sxs-lookup"><span data-stu-id="92a82-229">Run the sample</span></span>
<span data-ttu-id="92a82-230">Als u hebt het basisproject gebruikt of gevolgd samen met de procedure moet nu uw toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="92a82-230">If you've used the skeleton or followed along with the walkthrough your application should now run.</span></span> <span data-ttu-id="92a82-231">De simulator Start en op **aanmelden** om de toepassing te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="92a82-231">Start the simulator and click **Sign in** to use the application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="92a82-232">Beveiligingsupdates voor onze product</span><span class="sxs-lookup"><span data-stu-id="92a82-232">Get security updates for our product</span></span>
<span data-ttu-id="92a82-233">We raden u aan wanneer er beveiligingsincidenten door bezoeken optreden meldingen ontvangt de [Security TechCenter](https://technet.microsoft.com/security/dd252948) en u te abonneren op Security Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="92a82-233">We encourage you to get notifications of when security incidents occur by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

