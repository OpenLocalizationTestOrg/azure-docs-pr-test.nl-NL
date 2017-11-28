---
title: Ophalen van een token met behulp van een toepassing voor iOS - Azure AD B2C | Microsoft Docs
description: "In dit artikel wordt uitgelegd hoe u toocreate een iOS-app die gebruikmaakt van AppAuth met Azure Active Directory B2C toomanage gebruikers-id's en gebruikers te verifiëren."
services: active-directory-b2c
documentationcenter: ios
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: e7cbe2de6e9ae3d45448cdd36292c457a0ef4887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="6026b-103">Azure AD B2C: Meld u aan met een iOS-toepassing</span><span class="sxs-lookup"><span data-stu-id="6026b-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="6026b-104">Hallo Microsoft identity-platform gebruikt open standaarden, zoals OAuth2 en OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="6026b-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="6026b-105">Gebruik van een open standaard protocol biedt meer mogelijkheden voor ontwikkelaars bij het selecteren van een bibliotheek toointegrate met onze services.</span><span class="sxs-lookup"><span data-stu-id="6026b-105">Using an open standard protocol offers more developer choice when selecting a library toointegrate with our services.</span></span> <span data-ttu-id="6026b-106">We bieden in dit scenario en andere leuk tooaid ontwikkelaars met het schrijven van toepassingen die verbinding toohello Microsoft Identity-platform maken.</span><span class="sxs-lookup"><span data-stu-id="6026b-106">We've provided this walkthrough and others like it tooaid developers with writing applications that connect toohello Microsoft Identity platform.</span></span> <span data-ttu-id="6026b-107">De meeste bibliotheken die implementeren [hello RFC6749 OAuth2-specificatie](https://tools.ietf.org/html/rfc6749) zijn kunnen tooconnect toohello Microsoft Identity-platform.</span><span class="sxs-lookup"><span data-stu-id="6026b-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="6026b-108">Microsoft biedt geen oplossingen voor de bibliotheken van derden en een overzicht van deze bibliotheken niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6026b-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="6026b-109">Dit voorbeeld maakt gebruik van een derde partij bibliotheek aangeroepen AppAuth dat is getest op compatibiliteit in algemene scenario's met hello Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6026b-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="6026b-110">Problemen en functie-aanvragen moeten gerichte toohello-bibliotheek open source-project.</span><span class="sxs-lookup"><span data-stu-id="6026b-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="6026b-111">Raadpleeg [dit artikel](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6026b-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="6026b-112">Als u nieuwe tooOAuth2 of OpenID Connect, kan veel van deze voorbeeldconfiguratie veel tooyou zin niet maken.</span><span class="sxs-lookup"><span data-stu-id="6026b-112">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="6026b-113">We raden u een korte bekijkt [overzicht van het Hallo-protocol we hier hebt gedocumenteerd](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="6026b-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="6026b-114">Een Azure AD B2C-directory maken</span><span class="sxs-lookup"><span data-stu-id="6026b-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="6026b-115">Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken.</span><span class="sxs-lookup"><span data-stu-id="6026b-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="6026b-116">Een directory is een container voor alle gebruikers, apps en groepen.</span><span class="sxs-lookup"><span data-stu-id="6026b-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="6026b-117">Als u nog geen directory hebt, [maakt u een B2C-directory](active-directory-b2c-get-started.md) voordat u verdergaat.</span><span class="sxs-lookup"><span data-stu-id="6026b-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="6026b-118">Een app maken</span><span class="sxs-lookup"><span data-stu-id="6026b-118">Create an application</span></span>
<span data-ttu-id="6026b-119">Vervolgens moet u een app toocreate in uw B2C-directory.</span><span class="sxs-lookup"><span data-stu-id="6026b-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="6026b-120">Hallo app-registratie biedt informatie over het Azure AD dat het moet toocommunicate veilig met uw app.</span><span class="sxs-lookup"><span data-stu-id="6026b-120">hello app registration gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="6026b-121">Volg toocreate een mobiele app [deze instructies](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="6026b-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="6026b-122">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="6026b-122">Be sure to:</span></span>

* <span data-ttu-id="6026b-123">Omvatten een **Native client** in Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="6026b-123">Include a **Native client** in hello application.</span></span>
* <span data-ttu-id="6026b-124">Kopiëren Hallo **toepassings-ID** is toegewezen tooyour app.</span><span class="sxs-lookup"><span data-stu-id="6026b-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="6026b-125">U hebt deze GUID later nodig.</span><span class="sxs-lookup"><span data-stu-id="6026b-125">You need this GUID later.</span></span>
* <span data-ttu-id="6026b-126">Instellen van een **omleidings-URI** met een aangepast schema (bijvoorbeeld com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="6026b-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="6026b-127">U hebt deze URI later nodig.</span><span class="sxs-lookup"><span data-stu-id="6026b-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="6026b-128">Het beleid maken</span><span class="sxs-lookup"><span data-stu-id="6026b-128">Create your policies</span></span>
<span data-ttu-id="6026b-129">In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="6026b-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="6026b-130">Deze app bevat één identiteit ervaring: een gecombineerde aanmelden en registreren.</span><span class="sxs-lookup"><span data-stu-id="6026b-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="6026b-131">Maak van dit beleid, zoals beschreven in de [naslagartikel](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="6026b-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="6026b-132">Wanneer u Hallo beleid maakt, moet u:</span><span class="sxs-lookup"><span data-stu-id="6026b-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="6026b-133">Onder **registratiekenmerken**, selecteer Hallo kenmerk **weergavenaam**.</span><span class="sxs-lookup"><span data-stu-id="6026b-133">Under **Sign-up attributes**, select hello attribute **Display name**.</span></span>  <span data-ttu-id="6026b-134">U kunt ook andere kenmerken selecteren.</span><span class="sxs-lookup"><span data-stu-id="6026b-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="6026b-135">Onder **toepassingsclaims**, selecteert u de claims Hallo **weergavenaam** en **Object-ID van gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="6026b-135">Under **Application claims**, select hello claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="6026b-136">U kunt ook andere claims selecteren.</span><span class="sxs-lookup"><span data-stu-id="6026b-136">You can select other claims as well.</span></span>
* <span data-ttu-id="6026b-137">Kopiëren Hallo **naam** van elk beleid nadat u dit hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6026b-137">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="6026b-138">De beleidsnaam van uw wordt voorafgegaan door `b2c_1_` wanneer u Hallo beleid opslaat.</span><span class="sxs-lookup"><span data-stu-id="6026b-138">Your policy name is prefixed with `b2c_1_` when you save hello policy.</span></span>  <span data-ttu-id="6026b-139">U nodig beleidsnaam hello later.</span><span class="sxs-lookup"><span data-stu-id="6026b-139">You need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="6026b-140">Wanneer u uw beleid hebt gemaakt, bent u klaar toobuild uw app.</span><span class="sxs-lookup"><span data-stu-id="6026b-140">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="6026b-141">Hallo voorbeeldcode downloaden</span><span class="sxs-lookup"><span data-stu-id="6026b-141">Download hello sample code</span></span>
<span data-ttu-id="6026b-142">We hebben een werkende-voorbeeldtoepassing die gebruikmaakt van AppAuth met Azure AD B2C opgegeven [op GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="6026b-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="6026b-143">U kunt downloaden Hallo code en voer deze uit.</span><span class="sxs-lookup"><span data-stu-id="6026b-143">You can download hello code and run it.</span></span> <span data-ttu-id="6026b-144">toouse uw eigen Azure AD B2C-tenant, volg de instructies Hallo in Hallo [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="6026b-144">toouse your own Azure AD B2C tenant, follow hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="6026b-145">Dit voorbeeld is gemaakt door Hallo Leesmij-instructies te volgen door Hallo [AppAuth iOS-project op GitHub](https://github.com/openid/AppAuth-iOS).</span><span class="sxs-lookup"><span data-stu-id="6026b-145">This sample was created by following hello README instructions by hello [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="6026b-146">Voor meer informatie over de werking van Hallo-bibliotheek en Hallo voorbeelden Hallo verwijzing AppAuth README op GitHub.</span><span class="sxs-lookup"><span data-stu-id="6026b-146">For more details on how hello sample and hello library work, reference hello AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="6026b-147">Uw app toouse Azure AD B2C met AppAuth wijzigen</span><span class="sxs-lookup"><span data-stu-id="6026b-147">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="6026b-148">AppAuth biedt ondersteuning voor iOS 7 en hoger.</span><span class="sxs-lookup"><span data-stu-id="6026b-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="6026b-149">Sociale aanmeldingen op Google, SFSafariViewController toosupport is echter waarvoor iOS 9 of hoger vereist.</span><span class="sxs-lookup"><span data-stu-id="6026b-149">However, toosupport social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="6026b-150">Configuratie</span><span class="sxs-lookup"><span data-stu-id="6026b-150">Configuration</span></span>

<span data-ttu-id="6026b-151">U kunt de communicatie met Azure AD B2C configureren door te geven zowel Hallo autorisatie eindpunt en token eindpunt URI's.</span><span class="sxs-lookup"><span data-stu-id="6026b-151">You can configure communication with Azure AD B2C by specifying both hello authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="6026b-152">toogenerate deze URI's, moet u Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="6026b-152">toogenerate these URIs, you need hello following information:</span></span>
* <span data-ttu-id="6026b-153">Tenant-ID (bijvoorbeeld: contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="6026b-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="6026b-154">De naam van beleid (bijvoorbeeld B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="6026b-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="6026b-155">Hallo-tokeneindpunt URI kan worden gegenereerd door te vervangen Hallo Tenant\_-ID en het Hallo beleid\_naam in Hallo URL te volgen:</span><span class="sxs-lookup"><span data-stu-id="6026b-155">hello token endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="6026b-156">Hallo autorisatie eindpunt URI kan worden gegenereerd door te vervangen Hallo Tenant\_-ID en het Hallo beleid\_naam in Hallo URL te volgen:</span><span class="sxs-lookup"><span data-stu-id="6026b-156">hello authorization endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="6026b-157">Voer Hallo code toocreate na uw AuthorizationServiceConfiguration-object:</span><span class="sxs-lookup"><span data-stu-id="6026b-157">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="6026b-158">Autoriseren</span><span class="sxs-lookup"><span data-stu-id="6026b-158">Authorizing</span></span>

<span data-ttu-id="6026b-159">Na het configureren van of bij het ophalen van een configuratie van de service autorisatie, kan een autorisatieaanvraag worden samengesteld.</span><span class="sxs-lookup"><span data-stu-id="6026b-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="6026b-160">Hallo toocreate aanvragen, moet u de volgende informatie Hallo:</span><span class="sxs-lookup"><span data-stu-id="6026b-160">toocreate hello request, you need hello following information:</span></span>  
* <span data-ttu-id="6026b-161">Client-ID (bijvoorbeeld 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="6026b-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="6026b-162">Omleidings-URI met een aangepast schema (bijvoorbeeld com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span><span class="sxs-lookup"><span data-stu-id="6026b-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="6026b-163">Beide items moeten zijn opgeslagen als u zijn [u uw app registreert](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="6026b-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

<span data-ttu-id="6026b-164">tooset van uw toepassing toohandle Hallo omleiding toohello URI met het aangepaste schema hello, moet u tooupdate Hallo lijst met URL-schema in uw Info.pList:</span><span class="sxs-lookup"><span data-stu-id="6026b-164">tooset up your application toohandle hello redirect toohello URI with hello custom scheme, you need tooupdate hello list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="6026b-165">Open Info.pList.</span><span class="sxs-lookup"><span data-stu-id="6026b-165">Open Info.pList.</span></span>
* <span data-ttu-id="6026b-166">Beweeg de muisaanwijzer over een rij zoals bundel OS typecode en klikt u op Hallo \+ symbool.</span><span class="sxs-lookup"><span data-stu-id="6026b-166">Hover over a row like 'Bundle OS Type Code' and click hello \+ symbol.</span></span>
* <span data-ttu-id="6026b-167">Wijzig de naam Hallo nieuwe rij 'URL typen'.</span><span class="sxs-lookup"><span data-stu-id="6026b-167">Rename hello new row 'URL types'.</span></span>
* <span data-ttu-id="6026b-168">Klik op Hallo pijl toohello links van URL-types tooopen Hallo structuur.</span><span class="sxs-lookup"><span data-stu-id="6026b-168">Click hello arrow toohello left of 'URL types' tooopen hello tree.</span></span>
* <span data-ttu-id="6026b-169">Klik op Hallo pijl toohello links van '0-Item' tooopen Hallo structuur.</span><span class="sxs-lookup"><span data-stu-id="6026b-169">Click hello arrow toohello left of 'Item 0' tooopen hello tree.</span></span>
* <span data-ttu-id="6026b-170">Wijzig de naam van eerste item onder Item 0 too'URL regelingen.</span><span class="sxs-lookup"><span data-stu-id="6026b-170">Rename first item underneath Item 0 too'URL Schemes'.</span></span>
* <span data-ttu-id="6026b-171">Klik op Hallo pijl toohello links van URL-schema tooopen Hallo structuur.</span><span class="sxs-lookup"><span data-stu-id="6026b-171">Click hello arrow toohello left of 'URL Schemes' tooopen hello tree.</span></span>
* <span data-ttu-id="6026b-172">In de kolom 'Waarde' hello, is een leeg veld toohello links van '0 Item' onder de URL-schema.</span><span class="sxs-lookup"><span data-stu-id="6026b-172">In hello 'Value' column, there is a blank field toohello left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="6026b-173">De unieke schema Hallo waarde tooyour van de toepassing ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6026b-173">Set hello value tooyour application's unique scheme.</span></span>  <span data-ttu-id="6026b-174">Hallo-waarde moet overeenkomen met de Hallo dat wordt gebruikt in URL omleiding wanneer u Hallo OIDAuthorizationRequest object maakt.</span><span class="sxs-lookup"><span data-stu-id="6026b-174">hello value must match hello scheme used in redirectURL when creating hello OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="6026b-175">In ons voorbeeld hebben we com.onmicrosoft.fabrikamb2c.exampleapp' hello schema' gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6026b-175">In our sample, we used hello scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="6026b-176">Raadpleeg toohello [AppAuth handleiding](https://openid.github.io/AppAuth-iOS/) op hoe toocomplete Hallo rest van het Hallo-proces.</span><span class="sxs-lookup"><span data-stu-id="6026b-176">Refer toohello [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="6026b-177">Als u tooquickly moet aan de slag met een app werken, Bekijk [ons voorbeeld](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="6026b-177">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="6026b-178">Volg de stappen Hallo in Hallo [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter uw eigen Azure AD B2C-configuratie.</span><span class="sxs-lookup"><span data-stu-id="6026b-178">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="6026b-179">We zijn altijd open toofeedback en suggesties!</span><span class="sxs-lookup"><span data-stu-id="6026b-179">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="6026b-180">Als u problemen met dit onderwerp ondervindt of aanbevelingen voor het verbeteren van de inhoud hebben, zou wij stellen uw feedback Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="6026b-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="6026b-181">Voor functieaanvragen, toe te voegen te[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="6026b-181">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
