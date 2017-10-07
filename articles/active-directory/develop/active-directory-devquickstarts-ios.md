---
title: aaaIntegrate Azure AD in een iOS-app | Microsoft Docs
description: "Hoe beveiligd toobuild een iOS-toepassing die kan worden geïntegreerd met Azure AD voor aanmelden en Azure AD-aanroepen API's met behulp van OAuth."
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
ms.openlocfilehash: 6e05745b2b2b122995dcba896ab0f2ed32509e3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="333a2-103">Azure AD integreren met een iOS-app</span><span class="sxs-lookup"><span data-stu-id="333a2-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="333a2-104">Hallo Preview-versie van onze nieuwe [ontwikkelaarsportal](https://identity.microsoft.com/Docs/iOS) waarmee u leren werken met Azure Active Directory in een paar minuten!</span><span class="sxs-lookup"><span data-stu-id="333a2-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="333a2-105">Hallo-portal voor ontwikkelaars leidt u door het Hallo-proces voor het registreren van een app en Azure AD integreren in uw code.</span><span class="sxs-lookup"><span data-stu-id="333a2-105">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="333a2-106">Wanneer u klaar bent, hebt u een eenvoudige toepassing die gebruikers in uw tenant en een back-end die kunnen tokens accepteren en gevalideerd kan worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="333a2-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="333a2-107">Azure Active Directory (Azure AD) biedt Hallo Active Directory Authentication Library of ADAL voor iOS-clients hebt die tooaccess moeten bronnen beveiligde.</span><span class="sxs-lookup"><span data-stu-id="333a2-107">Azure Active Directory (Azure AD) provides hello Active Directory Authentication Library, or ADAL, for iOS clients that need tooaccess protected resources.</span></span> <span data-ttu-id="333a2-108">ADAL eenvoudiger Hallo dat uw app gebruikmaakt van tooobtain toegangstokens.</span><span class="sxs-lookup"><span data-stu-id="333a2-108">ADAL simplifies hello process that your app uses tooobtain access tokens.</span></span> <span data-ttu-id="333a2-109">toodemonstrate hoe eenvoudig het is in dit artikel wordt een takenlijst Objective-C-toepassing bouwt die:</span><span class="sxs-lookup"><span data-stu-id="333a2-109">toodemonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="333a2-110">Krijgt toegang tot tokens voor hello Azure AD Graph API aanroept met behulp van Hallo [OAuth 2.0-verificatieprotocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="333a2-110">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="333a2-111">Zoekt een directory voor gebruikers met een alias voor een gegeven.</span><span class="sxs-lookup"><span data-stu-id="333a2-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="333a2-112">toobuild hello volledige werkende toepassing, moet u:</span><span class="sxs-lookup"><span data-stu-id="333a2-112">toobuild hello complete working application, you need to:</span></span>

1. <span data-ttu-id="333a2-113">Uw toepassing registreren met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="333a2-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="333a2-114">Installeren en configureren van ADAL.</span><span class="sxs-lookup"><span data-stu-id="333a2-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="333a2-115">Gebruik ADAL tooget tokens van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="333a2-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="333a2-116">tooget gestart, [Hallo app basisproject downloaden](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) of [Hallo voltooid voorbeeld downloaden](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="333a2-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="333a2-117">U moet ook een Azure AD-tenant kunt u gebruikers maken en een toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="333a2-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="333a2-118">Als u niet al een tenant [meer informatie over hoe tooget een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="333a2-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="333a2-119">Hallo Preview-versie van onze nieuwe [ontwikkelaarsportal](https://identity.microsoft.com/Docs/iOS) waarmee u leren werken met Azure AD in een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="333a2-119">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="333a2-120">Hallo-portal voor ontwikkelaars leidt u door het Hallo-proces voor het registreren van een app en Azure AD integreren in uw code.</span><span class="sxs-lookup"><span data-stu-id="333a2-120">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="333a2-121">Wanneer u klaar bent, hebt u een eenvoudige toepassing die u kunt verificatie van gebruikers in uw tenant en een back-endnetwerk, kan tokens accepteren en valideren.</span><span class="sxs-lookup"><span data-stu-id="333a2-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="333a2-122">1. Bepalen welke uw omleidings-URI voor iOS is</span><span class="sxs-lookup"><span data-stu-id="333a2-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="333a2-123">toosecurely start uw toepassingen in bepaalde gevallen SSO, moet u een *omleidings-URI* in een bepaalde opmaak.</span><span class="sxs-lookup"><span data-stu-id="333a2-123">toosecurely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="333a2-124">Een omleidings-URI is gebruikte tooensure die Hallo tokens return toohello juiste toepassing die voor hen gevraagd.</span><span class="sxs-lookup"><span data-stu-id="333a2-124">A redirect URI is used tooensure that hello tokens return toohello correct application that asked for them.</span></span>


<span data-ttu-id="333a2-125">Hallo iOS-indeling voor een omleidings-URI is:</span><span class="sxs-lookup"><span data-stu-id="333a2-125">hello iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="333a2-126">**App-schema** -dit is geregistreerd in uw XCode-project.</span><span class="sxs-lookup"><span data-stu-id="333a2-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="333a2-127">Het is hoe andere toepassingen u kunnen aanroepen.</span><span class="sxs-lookup"><span data-stu-id="333a2-127">It is how other applications can call you.</span></span> <span data-ttu-id="333a2-128">U vindt dit onder Info.plist -> URL typen-URL-id >.</span><span class="sxs-lookup"><span data-stu-id="333a2-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="333a2-129">Als u nog een of meer geconfigureerd hebt, moet u een maken.</span><span class="sxs-lookup"><span data-stu-id="333a2-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="333a2-130">**bundel-id** -dit is bundel-id vinden onder 'id' hello ongedaan maken de projectinstellingen van uw in XCode.</span><span class="sxs-lookup"><span data-stu-id="333a2-130">**bundle-id** - This is hello Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="333a2-131">Een voorbeeld van deze Quick Start-code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span><span class="sxs-lookup"><span data-stu-id="333a2-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-hello-directorysearcher-application"></a><span data-ttu-id="333a2-132">2. Hallo DirectorySearcher toepassing registreren</span><span class="sxs-lookup"><span data-stu-id="333a2-132">2. Register hello DirectorySearcher application</span></span>
<span data-ttu-id="333a2-133">tooset van uw app-tokens tooget, moet u eerst tooregister in uw Azure AD-tenant en verleen deze machtiging tooaccess hello Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="333a2-133">tooset up your app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="333a2-134">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="333a2-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="333a2-135">Klik op de bovenste balk hello, uw account.</span><span class="sxs-lookup"><span data-stu-id="333a2-135">On hello top bar, click your account.</span></span> <span data-ttu-id="333a2-136">Onder Hallo **Directory** Hallo Active Directory-tenant waar u tooregister Kies uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="333a2-136">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="333a2-137">Klik op **meer Services** in Hallo meest linkse navigatievenster en selecteer vervolgens **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="333a2-137">Click **More Services** in hello leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="333a2-138">Klik op **App registraties**, en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="333a2-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="333a2-139">Ga als volgt Hallo vraagt toocreate een nieuwe **systeemeigen clienttoepassing**.</span><span class="sxs-lookup"><span data-stu-id="333a2-139">Follow hello prompts toocreate a new **Native Client Application**.</span></span>
  * <span data-ttu-id="333a2-140">Hallo **naam** Hallo toepassing beschrijving van uw toepassing tooend gebruikers.</span><span class="sxs-lookup"><span data-stu-id="333a2-140">hello **Name** of hello application describes your application tooend users.</span></span>
  * <span data-ttu-id="333a2-141">Hallo **omleidings-Uri** is een schema en de tekenreeks combinatie dat gebruikmaakt van Azure AD tooreturn token antwoorden.</span><span class="sxs-lookup"><span data-stu-id="333a2-141">hello **Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span>  <span data-ttu-id="333a2-142">Voer een waarde die specifieke tooyour toepassing is en is gebaseerd op Hallo vorige omleidings-URI informatie.</span><span class="sxs-lookup"><span data-stu-id="333a2-142">Enter a value that is specific tooyour application and is based on hello previous redirect URI information.</span></span>
6. <span data-ttu-id="333a2-143">Nadat u Hallo-registratie hebt voltooid, wijst Azure AD van uw app een unieke toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="333a2-143">After you've completed hello registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="333a2-144">U moet deze waarde in de volgende secties hello, dus kopieer het van Hallo toepassingstabblad.</span><span class="sxs-lookup"><span data-stu-id="333a2-144">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="333a2-145">Van Hallo **instellingen** pagina **Required Permissions** en selecteer vervolgens **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="333a2-145">From hello **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="333a2-146">Selecteer **Microsoft Graph** zoals Hallo API, en voeg vervolgens Hallo **Directory-gegevens lezen** machtiging onder **gedelegeerde machtigingen**.</span><span class="sxs-lookup"><span data-stu-id="333a2-146">Select **Microsoft Graph** as hello API, and then add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="333a2-147">Hiermee stelt u uw toepassing tooquery hello Azure AD Graph API voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="333a2-147">This sets up your application tooquery hello Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="333a2-148">3. Installeren en configureren van ADAL</span><span class="sxs-lookup"><span data-stu-id="333a2-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="333a2-149">Nu dat u een toepassing in Azure AD hebt, kunt u ADAL installeert en uw identiteitsgerelateerde code schrijven.</span><span class="sxs-lookup"><span data-stu-id="333a2-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="333a2-150">ADAL toocommunicate met Azure AD, moet u tooprovide met enige informatie over de registratie van uw app.</span><span class="sxs-lookup"><span data-stu-id="333a2-150">For ADAL toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

1. <span data-ttu-id="333a2-151">Beginnen met het toevoegen van ADAL toohello DirectorySearcher project via CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="333a2-151">Begin by adding ADAL toohello DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="333a2-152">Hallo toothis podfile volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="333a2-152">Add hello following toothis podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="333a2-153">Nu laden Hallo podfile via CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="333a2-153">Now load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="333a2-154">Deze stap maakt een nieuwe XCode-werkruimte die u hebt geladen.</span><span class="sxs-lookup"><span data-stu-id="333a2-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="333a2-155">Open Hallo plist-bestand in Hallo Quick Start-project, `settings.plist`.</span><span class="sxs-lookup"><span data-stu-id="333a2-155">In hello QuickStart project, open hello plist file `settings.plist`.</span></span>  <span data-ttu-id="333a2-156">Vervang de waarden Hallo Hallo-elementen in Hallo sectie tooreflect Hallo waarden die u hebt ingevoerd in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="333a2-156">Replace hello values of hello elements in hello section tooreflect hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="333a2-157">Uw code verwijst naar deze waarden wanneer deze gebruikmaakt van ADAL.</span><span class="sxs-lookup"><span data-stu-id="333a2-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="333a2-158">Hallo `tenant` Hallo domein van uw Azure AD-tenant, bijvoorbeeld: contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="333a2-158">hello `tenant` is hello domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="333a2-159">Hallo `clientId` Hallo client-ID van uw toepassing die u hebt gekopieerd uit de portal Hallo is.</span><span class="sxs-lookup"><span data-stu-id="333a2-159">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="333a2-160">Hallo `redirectUri` Hallo Omleidings-URL die u hebt geregistreerd in de portal Hallo is.</span><span class="sxs-lookup"><span data-stu-id="333a2-160">hello `redirectUri` is hello redirect URL that you registered in hello portal.</span></span>

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="333a2-161">4.    Gebruik van ADAL tooget tokens van Azure AD</span><span class="sxs-lookup"><span data-stu-id="333a2-161">4.    Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="333a2-162">Hallo basisprincipe achter ADAL is dat wanneer uw app een toegangstoken moet, een completionBlock aanroept `+(void) getToken : `, en ADAL Hallo rest.</span><span class="sxs-lookup"><span data-stu-id="333a2-162">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="333a2-163">In Hallo `QuickStart` project, open `GraphAPICaller.m` en zoek Hallo `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` Opmerking bij Hallo bovenkant.</span><span class="sxs-lookup"><span data-stu-id="333a2-163">In hello `QuickStart` project, open `GraphAPICaller.m` and locate hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near hello top.</span></span>  <span data-ttu-id="333a2-164">Dit is waar u doorgeven ADAL Hallo coördinaten via een CompletionBlock, toocommunicate met Azure AD en meer over toocache tokens.</span><span class="sxs-lookup"><span data-stu-id="333a2-164">This is where you pass ADAL hello coordinates through a CompletionBlock, toocommunicate with Azure AD, and tell it how toocache tokens.</span></span>

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
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy toodisplay hello correct mobile UX. You most likely won't need it in your code.
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

2. <span data-ttu-id="333a2-165">Er moet nu toouse dit token toosearch voor gebruikers in het Hallo-grafiek.</span><span class="sxs-lookup"><span data-stu-id="333a2-165">Now we need toouse this token toosearch for users in hello graph.</span></span> <span data-ttu-id="333a2-166">Hallo zoeken `// TODO: implement SearchUsersList` opmerking.</span><span class="sxs-lookup"><span data-stu-id="333a2-166">Find hello `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="333a2-167">Deze methode maakt een GET-aanvraag toohello Azure AD Graph API tooquery voor gebruikers wiens UPN met de Hallo zoekterm opgegeven begint.</span><span class="sxs-lookup"><span data-stu-id="333a2-167">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="333a2-168">tooquery hello Azure AD Graph API, moet u een access_token in Hallo tooinclude `Authorization` koptekst van Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="333a2-168">tooquery hello Azure AD Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request.</span></span> <span data-ttu-id="333a2-169">Dit is waar de ADAL wordt geleverd.</span><span class="sxs-lookup"><span data-stu-id="333a2-169">This is where ADAL comes in.</span></span>

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

                         // We can grab hello JSON node at hello top tooget our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by hello key name being "value". It really is hello name of the
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


3. <span data-ttu-id="333a2-170">Wanneer uw app een token aanvragen door het aanroepen van `getToken(...)`, ADAL probeert een token tooreturn zonder Hallo gebruiker wordt gevraagd om referenties.</span><span class="sxs-lookup"><span data-stu-id="333a2-170">When your app requests a token by calling `getToken(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="333a2-171">Als ADAL dat die gebruiker Hallo moet toosign in een token tooget vaststelt, wordt deze weergegeven in het dialoogvenster voor aanmelding, Hallo gebruikersreferenties verzamelen en retourneert een token na een geslaagde authenticatie.</span><span class="sxs-lookup"><span data-stu-id="333a2-171">If ADAL determines that hello user needs toosign in tooget a token, it will display a dialog box for sign-in, collect hello user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="333a2-172">Als ADAL niet kunnen tooreturn een token voor een bepaalde reden, genereert een `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="333a2-172">If ADAL is not able tooreturn a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="333a2-173">Hallo `AuthenticationResult` object bevat een `tokenCacheStoreItem` -object dat kan worden gebruikt toocollect Hallo informatie die uw app mogelijk nodig.</span><span class="sxs-lookup"><span data-stu-id="333a2-173">hello `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used toocollect hello information that your app may need.</span></span> <span data-ttu-id="333a2-174">In de Quick Start, Hallo `tokenCacheStoreItem` gebruikte toodetermine is als verificatie is al voltooid.</span><span class="sxs-lookup"><span data-stu-id="333a2-174">In hello QuickStart, `tokenCacheStoreItem` is used toodetermine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-hello-application"></a><span data-ttu-id="333a2-175">5. Hallo-toepassing bouwen en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="333a2-175">5. Build and run hello application</span></span>
<span data-ttu-id="333a2-176">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="333a2-176">Congratulations!</span></span> <span data-ttu-id="333a2-177">U hebt nu een werkende iOS-toepassing kunt verificatie van gebruikers, veilig aanroepen van Web-API's met behulp van OAuth 2.0 en basisinformatie over Hallo gebruiker ophalen.</span><span class="sxs-lookup"><span data-stu-id="333a2-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="333a2-178">Als u nog niet gedaan hebt, is nu Hallo tijd toopopulate uw tenant waarbij sommige gebruikers.</span><span class="sxs-lookup"><span data-stu-id="333a2-178">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="333a2-179">Start uw app Quick Start en vervolgens weer aanmelden met een van deze gebruikers.</span><span class="sxs-lookup"><span data-stu-id="333a2-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="333a2-180">Zoeken naar andere gebruikers op basis van de UPN.</span><span class="sxs-lookup"><span data-stu-id="333a2-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="333a2-181">Hallo-app sluiten en opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="333a2-181">Close hello app, and then start it again.</span></span>  <span data-ttu-id="333a2-182">U ziet dat Hallo gebruikerssessie intact blijft.</span><span class="sxs-lookup"><span data-stu-id="333a2-182">Notice that hello user's session remains intact.</span></span>

<span data-ttu-id="333a2-183">ADAL maakt het eenvoudig tooincorporate al deze algemene identiteit functies in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="333a2-183">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="333a2-184">Dit zorgt voor alle Hallo dirty werk voor u, zoals het Cachebeheer van de OAuth-protocolondersteuning, Hallo-gebruiker met een gebruikersinterface toosign in presenteren en vernieuwen van tokens verlopen.</span><span class="sxs-lookup"><span data-stu-id="333a2-184">It takes care of all hello dirty work for you, like cache management, OAuth protocol support, presenting hello user with a UI toosign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="333a2-185">Alles wat u moet tooknow één API-aanroep is `getToken`.</span><span class="sxs-lookup"><span data-stu-id="333a2-185">All you really need tooknow is a single API call, `getToken`.</span></span>

<span data-ttu-id="333a2-186">Ter referentie: Hallo voltooid voorbeeld (zonder uw configuratiewaarden) wordt aangeboden op [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="333a2-186">For reference, hello completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="333a2-187">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="333a2-187">Next steps</span></span>
<span data-ttu-id="333a2-188">U kunt nu verplaatsen op tooadditional scenario's.</span><span class="sxs-lookup"><span data-stu-id="333a2-188">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="333a2-189">U kunt tootry:</span><span class="sxs-lookup"><span data-stu-id="333a2-189">You may want tootry:</span></span>

* [<span data-ttu-id="333a2-190">Een Node.JS-Web-API met Azure AD beveiligen</span><span class="sxs-lookup"><span data-stu-id="333a2-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="333a2-191">Meer informatie over [hoe tooenable SSO cross-app voor iOS met ADAL](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="333a2-191">Learn [how tooenable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

