---
title: Azure AD integreren met een iOS-app | Microsoft Docs
description: "Het bouwen van een iOS-toepassing die kan worden geïntegreerd met Azure AD voor aanmelden en Azure AD-aanroepen beveiligd API's met behulp van OAuth."
services: active-directory
documentationcenter: ios
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 57f465df99ac234466459b8031f61805d8334b59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="e6c2f-103">Azure AD integreren met een iOS-app</span><span class="sxs-lookup"><span data-stu-id="e6c2f-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="e6c2f-104">Deze Preview-versie van onze nieuwe [ontwikkelaarsportal](https://identity.microsoft.com/Docs/iOS) waarmee u leren werken met Azure Active Directory in een paar minuten!</span><span class="sxs-lookup"><span data-stu-id="e6c2f-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="e6c2f-105">De portal voor ontwikkelaars leidt u door het proces van registreren van een app en Azure AD integreren in uw code.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-105">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="e6c2f-106">Wanneer u klaar bent, hebt u een eenvoudige toepassing die gebruikers in uw tenant en een back-end die kunnen tokens accepteren en gevalideerd kan worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="e6c2f-107">Azure Active Directory (Azure AD) biedt de Active Directory Authentication Library of ADAL voor iOS-clients die toegang moeten krijgen tot beveiligde bronnen.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-107">Azure Active Directory (Azure AD) provides the Active Directory Authentication Library, or ADAL, for iOS clients that need to access protected resources.</span></span> <span data-ttu-id="e6c2f-108">ADAL vereenvoudigt het proces dat uw app gebruikmaakt van toegangstokens te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-108">ADAL simplifies the process that your app uses to obtain access tokens.</span></span> <span data-ttu-id="e6c2f-109">Om te demonstreren hoe eenvoudig het is, in dit artikel gaan we verder met een takenlijst Objective-C-toepassing die:</span><span class="sxs-lookup"><span data-stu-id="e6c2f-109">To demonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="e6c2f-110">Krijgt toegang tot tokens voor de Azure AD Graph-API aanroept met behulp van de [OAuth 2.0-verificatieprotocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="e6c2f-110">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="e6c2f-111">Zoekt een directory voor gebruikers met een alias voor een gegeven.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="e6c2f-112">De volledige werkende toepassing bouwen, moet u:</span><span class="sxs-lookup"><span data-stu-id="e6c2f-112">To build the complete working application, you need to:</span></span>

1. <span data-ttu-id="e6c2f-113">Uw toepassing registreren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="e6c2f-114">Installeren en configureren van ADAL.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="e6c2f-115">ADAL gebruikt om tokens van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="e6c2f-116">Aan de slag [de basis van de app downloaden](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) of [het voltooide voorbeeld downloaden](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="e6c2f-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="e6c2f-117">U moet ook een Azure AD-tenant kunt u gebruikers maken en een toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="e6c2f-118">Als u niet al een tenant [Lees hoe u een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="e6c2f-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="e6c2f-119">Deze Preview-versie van onze nieuwe [ontwikkelaarsportal](https://identity.microsoft.com/Docs/iOS) waarmee u leren werken met Azure AD in een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-119">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="e6c2f-120">De portal voor ontwikkelaars leidt u door het proces van registreren van een app en Azure AD integreren in uw code.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-120">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="e6c2f-121">Wanneer u klaar bent, hebt u een eenvoudige toepassing die u kunt verificatie van gebruikers in uw tenant en een back-endnetwerk, kan tokens accepteren en valideren.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="e6c2f-122">1. Bepalen welke uw omleidings-URI voor iOS is</span><span class="sxs-lookup"><span data-stu-id="e6c2f-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="e6c2f-123">U start uw toepassingen veilig in bepaalde SSO-scenario's, moet u een *omleidings-URI* in een bepaalde opmaak.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-123">To securely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="e6c2f-124">Een omleidings-URI wordt gebruikt om ervoor te zorgen dat de tokens terugkeren naar de juiste toepassing die voor hen gevraagd.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-124">A redirect URI is used to ensure that the tokens return to the correct application that asked for them.</span></span>


<span data-ttu-id="e6c2f-125">De iOS-indeling voor een omleidings-URI is:</span><span class="sxs-lookup"><span data-stu-id="e6c2f-125">The iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="e6c2f-126">**App-schema** -dit is geregistreerd in uw XCode-project.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="e6c2f-127">Het is hoe andere toepassingen u kunnen aanroepen.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-127">It is how other applications can call you.</span></span> <span data-ttu-id="e6c2f-128">U vindt dit onder Info.plist -> URL typen-URL-id >.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="e6c2f-129">Als u nog een of meer geconfigureerd hebt, moet u een maken.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="e6c2f-130">**bundel-id** -dit is de bundel-id vinden onder 'id' ongedaan maken de projectinstellingen van uw in XCode.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-130">**bundle-id** - This is the Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="e6c2f-131">Een voorbeeld van deze Quick Start-code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span><span class="sxs-lookup"><span data-stu-id="e6c2f-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-the-directorysearcher-application"></a><span data-ttu-id="e6c2f-132">2. De toepassing DirectorySearcher registreren</span><span class="sxs-lookup"><span data-stu-id="e6c2f-132">2. Register the DirectorySearcher application</span></span>
<span data-ttu-id="e6c2f-133">Als u uw app om op te halen van tokens instelt, moet u eerst registreren in uw Azure AD-tenant en verleent deze machtiging voor toegang tot de Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="e6c2f-133">To set up your app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="e6c2f-134">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e6c2f-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e6c2f-135">Klik op uw account op de bovenste balk.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-135">On the top bar, click your account.</span></span> <span data-ttu-id="e6c2f-136">Onder de **Directory** kiest u de Active Directory-tenant waar u uw toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-136">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>
3. <span data-ttu-id="e6c2f-137">Klik op **meer Services** in de meest linkse navigatievenster en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-137">Click **More Services** in the leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="e6c2f-138">Klik op **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="e6c2f-139">Volg de aanwijzingen voor het maken van een nieuwe **systeemeigen clienttoepassing**.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-139">Follow the prompts to create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="e6c2f-140">De **naam** beschrijving van de toepassing van uw toepassing aan eindgebruikers.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-140">The **Name** of the application describes your application to end users.</span></span>
  * <span data-ttu-id="e6c2f-141">De **omleidings-Uri** is een combinatie schema en de tekenreeks die gebruikmaakt van Azure AD token antwoorden retourneren.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-141">The **Redirect Uri** is a scheme and string combination that Azure AD uses to return token responses.</span></span>  <span data-ttu-id="e6c2f-142">Voer een waarde die specifiek is voor uw toepassing en is gebaseerd op de vorige omleidings-URI-gegevens.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-142">Enter a value that is specific to your application and is based on the previous redirect URI information.</span></span>
6. <span data-ttu-id="e6c2f-143">Nadat u de registratie hebt voltooid, wijst Azure AD van uw app een unieke toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-143">After you've completed the registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="e6c2f-144">U moet deze waarde in de volgende secties, dus kopiëren vanaf het toepassingstabblad.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-144">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="e6c2f-145">Van de **instellingen** pagina **Required Permissions** en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-145">From the **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="e6c2f-146">Selecteer **Microsoft Graph** als de API en voeg vervolgens de **Directory-gegevens lezen** machtiging onder **gedelegeerde machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-146">Select **Microsoft Graph** as the API, and then add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="e6c2f-147">Hiermee stelt u uw toepassing query uitvoeren op de Azure AD Graph API voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-147">This sets up your application to query the Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="e6c2f-148">3. Installeren en configureren van ADAL</span><span class="sxs-lookup"><span data-stu-id="e6c2f-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="e6c2f-149">Nu dat u een toepassing in Azure AD hebt, kunt u ADAL installeert en uw identiteitsgerelateerde code schrijven.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="e6c2f-150">Voor ADAL om te communiceren met Azure AD, moet u voorzien enige informatie over de registratie van uw app.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-150">For ADAL to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

1. <span data-ttu-id="e6c2f-151">Beginnen met het ADAL toevoegen aan het project DirectorySearcher via CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-151">Begin by adding ADAL to the DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="e6c2f-152">Voeg het volgende aan de podfile toe:</span><span class="sxs-lookup"><span data-stu-id="e6c2f-152">Add the following to this podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="e6c2f-153">Nu de podfile laden via CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-153">Now load the podfile by using CocoaPods.</span></span> <span data-ttu-id="e6c2f-154">Deze stap maakt een nieuwe XCode-werkruimte die u hebt geladen.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="e6c2f-155">Open het plist-bestand in de Quick Start-project `settings.plist`.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-155">In the QuickStart project, open the plist file `settings.plist`.</span></span>  <span data-ttu-id="e6c2f-156">Vervang de waarden van de elementen in de sectie in overeenstemming met de waarden die u hebt ingevoerd in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-156">Replace the values of the elements in the section to reflect the values that you entered in the Azure portal.</span></span> <span data-ttu-id="e6c2f-157">Uw code verwijst naar deze waarden wanneer deze gebruikmaakt van ADAL.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="e6c2f-158">De `tenant` is het domein van uw Azure AD-tenant, bijvoorbeeld: contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-158">The `tenant` is the domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="e6c2f-159">De `clientId` is de client-ID van uw toepassing die u hebt gekopieerd uit de portal.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-159">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="e6c2f-160">De `redirectUri` is de omleidings-URL die u hebt geregistreerd in de portal.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-160">The `redirectUri` is the redirect URL that you registered in the portal.</span></span>

## <a name="4----use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="e6c2f-161">4.    Gebruikmaken van ADAL voor het ophalen van tokens van Azure AD</span><span class="sxs-lookup"><span data-stu-id="e6c2f-161">4.    Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="e6c2f-162">Het basisprincipe achter ADAL is dat wanneer uw app een toegangstoken moet, een completionBlock aanroept `+(void) getToken : `, en doet de rest van ADAL.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-162">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="e6c2f-163">In de `QuickStart` project, open `GraphAPICaller.m` en zoek de `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` opmerking aan de bovenkant.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-163">In the `QuickStart` project, open `GraphAPICaller.m` and locate the `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near the top.</span></span>  <span data-ttu-id="e6c2f-164">Dit is waar het doorgeven van ADAL de coördinaten via een CompletionBlock, om te communiceren met Azure AD en hoe deze tokens in de cache.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-164">This is where you pass ADAL the coordinates through a CompletionBlock, to communicate with Azure AD, and tell it how to cache tokens.</span></span>

    ```ObjC
    +(void) getToken : (BOOL) clearCache
               parent:(UIViewController*) parent
    completionHandler:(void (^) (NSString*, NSError*))completionBlock;
    {
        AppData* data = [AppData getInstance];
        if(data.userItem){
            completionBlock(data.userItem.accessToken, nil);
            return;
        }

        ADAuthenticationError *error;
        authContext = [ADAuthenticationContext authenticationContextWithAuthority:data.authority error:&error];
        authContext.parentController = parent;
        NSURL *redirectUri = [[NSURL alloc]initWithString:data.redirectUriString];

        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:data.resourceId
                                     clientId:data.clientId
                                  redirectUri:redirectUri
                               promptBehavior:AD_PROMPT_AUTO
                                       userId:data.userItem.userInformation.userId
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy to display the correct mobile UX. You most likely won't need it in your code.
                             completionBlock:^(ADAuthenticationResult *result) {

                                  if (result.status != AD_SUCCEEDED)
                                  {
                                     completionBlock(nil, result.error);
                                  }
                                  else
                                  {
                                      data.userItem = result.tokenCacheStoreItem;
                                      completionBlock(result.tokenCacheStoreItem.accessToken, nil);
                                  }
                             }];
    }

    ```

2. <span data-ttu-id="e6c2f-165">Nu moet dit token gebruiken om te zoeken naar gebruikers in de grafiek.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-165">Now we need to use this token to search for users in the graph.</span></span> <span data-ttu-id="e6c2f-166">Zoek de `// TODO: implement SearchUsersList` opmerking.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-166">Find the `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="e6c2f-167">Deze methode maakt een GET-aanvraag voor Azure AD Graph API aan query voor gebruikers wiens UPN met de opgegeven zoekterm begint.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-167">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="e6c2f-168">Om te vragen van de Azure AD Graph API, moet u een access_token in de `Authorization` koptekst van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-168">To query the Azure AD Graph API, you need to include an access_token in the `Authorization` header of the request.</span></span> <span data-ttu-id="e6c2f-169">Dit is waar de ADAL wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-169">This is where ADAL comes in.</span></span>

    ```ObjC
    +(void) searchUserList:(NSString*)searchString
                    parent:(UIViewController*) parent
          completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
    {
        if (!loadedApplicationSettings)
       {
            [self readApplicationSettings];
        }
        
        AppData* data = [AppData getInstance];

        NSString *graphURL = [NSString stringWithFormat:@"%@%@/users?api-version=%@&$filter=startswith(userPrincipalName, '%@')", data.taskWebApiUrlString, data.tenant, data.apiversion, searchString];

        [self craftRequest:[self.class trimString:graphURL]
                    parent:parent
         completionHandler:^(NSMutableURLRequest *request, NSError *error) {

             if (error != nil)
             {
                 completionBlock(nil, error);
             }
             else
             {

                 NSOperationQueue *queue = [[NSOperationQueue alloc]init];

                 [NSURLConnection sendAsynchronousRequest:request queue:queue completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {

                     if (error == nil && data != nil){

                         NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];

                         // We can grab the JSON node at the top to get our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by the key name being "value". It really is the name of the
                         // first node. :-)

                         // Each object is a key value pair
                         NSDictionary *keyValuePairs;
                         NSMutableArray* Users = [[NSMutableArray alloc]init];

                         for(int i =0; i < graphDataArray.count; i++)
                         {
                             keyValuePairs = [graphDataArray objectAtIndex:i];

                             User *s = [[User alloc]init];
                             s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                             s.name =[keyValuePairs valueForKey:@"givenName"];

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
         }];

    }

    ```


3. <span data-ttu-id="e6c2f-170">Wanneer uw app een token aanvragen door het aanroepen van `getToken(...)`, ADAL probeert te retourneren van een token zonder dat de gebruiker om referenties gevraagd.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-170">When your app requests a token by calling `getToken(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="e6c2f-171">Als ADAL wordt vastgesteld dat de gebruiker zich aanmelden moet bij een token verkrijgen, wordt deze weergegeven in het dialoogvenster voor aanmelding, verzamelen van referenties van de gebruiker en retourneert een token na een geslaagde authenticatie.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-171">If ADAL determines that the user needs to sign in to get a token, it will display a dialog box for sign-in, collect the user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="e6c2f-172">Als ADAL niet kan worden geretourneerd van een token voor een bepaalde reden, genereert een `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-172">If ADAL is not able to return a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="e6c2f-173">De `AuthenticationResult` object bevat een `tokenCacheStoreItem` -object dat kan worden gebruikt voor het verzamelen van de informatie die uw app mogelijk nodig.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-173">The `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used to collect the information that your app may need.</span></span> <span data-ttu-id="e6c2f-174">In de snelstartgids `tokenCacheStoreItem` wordt gebruikt om te bepalen of de verificatie al wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-174">In the QuickStart, `tokenCacheStoreItem` is used to determine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-the-application"></a><span data-ttu-id="e6c2f-175">5. De toepassing bouwen en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-175">5. Build and run the application</span></span>
<span data-ttu-id="e6c2f-176">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-176">Congratulations!</span></span> <span data-ttu-id="e6c2f-177">U hebt nu een werkende iOS-toepassing kunt verificatie van gebruikers, veilig aanroepen van Web-API's met behulp van OAuth 2.0 en algemene informatie over de gebruiker ophalen.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="e6c2f-178">Als u nog niet gedaan hebt, is nu de tijd voor het vullen van uw tenant waarbij sommige gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-178">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="e6c2f-179">Start uw app Quick Start en vervolgens weer aanmelden met een van deze gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="e6c2f-180">Zoeken naar andere gebruikers op basis van de UPN.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="e6c2f-181">Sluit de app en start het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-181">Close the app, and then start it again.</span></span>  <span data-ttu-id="e6c2f-182">U ziet dat de gebruikerssessie intact blijft.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-182">Notice that the user's session remains intact.</span></span>

<span data-ttu-id="e6c2f-183">ADAL kunt eenvoudig gebruikmaken van al deze algemene identiteit functies in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-183">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="e6c2f-184">Dit zorgt voor al het werk dirty voor u, zoals het Cachebeheer van de OAuth-protocolondersteuning, dat de gebruiker een gebruikersinterface aan te melden, en vernieuwen van tokens verlopen.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-184">It takes care of all the dirty work for you, like cache management, OAuth protocol support, presenting the user with a UI to sign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="e6c2f-185">Alles wat u moet weten één API-aanroep is `getToken`.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-185">All you really need to know is a single API call, `getToken`.</span></span>

<span data-ttu-id="e6c2f-186">Voor een verwijzing naar het voltooide voorbeeld (zonder uw configuratiewaarden) wordt aangeboden op [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="e6c2f-186">For reference, the completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="e6c2f-187">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e6c2f-187">Next steps</span></span>
<span data-ttu-id="e6c2f-188">U kunt nu verder met aanvullende scenario's.</span><span class="sxs-lookup"><span data-stu-id="e6c2f-188">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="e6c2f-189">U wilt proberen:</span><span class="sxs-lookup"><span data-stu-id="e6c2f-189">You may want to try:</span></span>

* [<span data-ttu-id="e6c2f-190">Een Node.JS-Web-API met Azure AD beveiligen</span><span class="sxs-lookup"><span data-stu-id="e6c2f-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="e6c2f-191">Meer informatie over [het inschakelen van eenmalige aanmelding voor cross-app voor iOS met ADAL](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="e6c2f-191">Learn [how to enable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

