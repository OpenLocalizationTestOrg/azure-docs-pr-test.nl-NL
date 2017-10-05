---
title: Ophalen van een token met behulp van een toepassing voor iOS - Azure AD B2C | Microsoft Docs
description: "In dit artikel wordt beschreven hoe u een iOS-app die gebruikmaakt van AppAuth met Azure Active Directory B2C gebruikersidentiteiten te beheren en verifiëren van gebruikers te maken."
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
ms.openlocfilehash: ebec5d910b8987dcc8155cd4ead00f87d219941c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="4191f-103">Azure AD B2C: Meld u aan met een iOS-toepassing</span><span class="sxs-lookup"><span data-stu-id="4191f-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="4191f-104">Op het Microsoft Identity-platform wordt gebruikgemaakt van open standaarden, zoals OAuth2 en OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="4191f-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="4191f-105">Gebruik van een open standaard protocol biedt meer mogelijkheden voor ontwikkelaars bij het selecteren van een bibliotheek integreren met onze services.</span><span class="sxs-lookup"><span data-stu-id="4191f-105">Using an open standard protocol offers more developer choice when selecting a library to integrate with our services.</span></span> <span data-ttu-id="4191f-106">We bieden in dit scenario en andere zoals deze ontwikkelaars helpen bij het schrijven van toepassingen die verbinding met de Microsoft Identity-platform maken.</span><span class="sxs-lookup"><span data-stu-id="4191f-106">We've provided this walkthrough and others like it to aid developers with writing applications that connect to the Microsoft Identity platform.</span></span> <span data-ttu-id="4191f-107">De meeste bibliotheken die implementeren [de RFC6749 OAuth2-specificatie](https://tools.ietf.org/html/rfc6749) kunnen geen verbinding maken met de Microsoft Identity-platform.</span><span class="sxs-lookup"><span data-stu-id="4191f-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="4191f-108">Microsoft biedt geen oplossingen voor de bibliotheken van derden en een overzicht van deze bibliotheken niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4191f-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="4191f-109">Dit voorbeeld maakt gebruik van een derde partij bibliotheek aangeroepen AppAuth dat is getest op compatibiliteit in algemene scenario's met de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="4191f-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="4191f-110">Problemen en functie-aanvragen moeten worden omgeleid naar de bibliotheek open source-project.</span><span class="sxs-lookup"><span data-stu-id="4191f-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="4191f-111">Raadpleeg [dit artikel](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4191f-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="4191f-112">Als u geen ervaring met OAuth2 of OpenID Connect, wellicht veel van de configuratie van deze niet verstandig veel voor u.</span><span class="sxs-lookup"><span data-stu-id="4191f-112">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="4191f-113">U wordt geadviseerd eerst een beknopt [overzicht van het hier gedocumenteerde protocol te bekijken](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="4191f-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="4191f-114">Een Azure AD B2C-directory maken</span><span class="sxs-lookup"><span data-stu-id="4191f-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="4191f-115">Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken.</span><span class="sxs-lookup"><span data-stu-id="4191f-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="4191f-116">Een directory is een container voor alle gebruikers, apps en groepen.</span><span class="sxs-lookup"><span data-stu-id="4191f-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="4191f-117">Als u nog geen directory hebt, [maakt u een B2C-directory](active-directory-b2c-get-started.md) voordat u verdergaat.</span><span class="sxs-lookup"><span data-stu-id="4191f-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="4191f-118">Een app maken</span><span class="sxs-lookup"><span data-stu-id="4191f-118">Create an application</span></span>
<span data-ttu-id="4191f-119">Vervolgens maakt u een app in uw B2C-directory.</span><span class="sxs-lookup"><span data-stu-id="4191f-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="4191f-120">De app-registratie biedt Azure AD-informatie die nodig is om veilig te communiceren met uw app.</span><span class="sxs-lookup"><span data-stu-id="4191f-120">The app registration gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="4191f-121">Volg voor het maken van een mobiele app [deze instructies](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="4191f-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="4191f-122">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="4191f-122">Be sure to:</span></span>

* <span data-ttu-id="4191f-123">Omvatten een **Native client** in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="4191f-123">Include a **Native client** in the application.</span></span>
* <span data-ttu-id="4191f-124">U de **toepassings-id** kopieert die is toegewezen aan uw app.</span><span class="sxs-lookup"><span data-stu-id="4191f-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="4191f-125">U hebt deze GUID later nodig.</span><span class="sxs-lookup"><span data-stu-id="4191f-125">You need this GUID later.</span></span>
* <span data-ttu-id="4191f-126">Instellen van een **omleidings-URI** met een aangepast schema (bijvoorbeeld com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="4191f-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="4191f-127">U hebt deze URI later nodig.</span><span class="sxs-lookup"><span data-stu-id="4191f-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="4191f-128">Het beleid maken</span><span class="sxs-lookup"><span data-stu-id="4191f-128">Create your policies</span></span>
<span data-ttu-id="4191f-129">In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4191f-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="4191f-130">Deze app bevat één identiteit ervaring: een gecombineerde aanmelden en registreren.</span><span class="sxs-lookup"><span data-stu-id="4191f-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="4191f-131">Maak van dit beleid, zoals beschreven in de [naslagartikel](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="4191f-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="4191f-132">Wanneer u het beleid maakt:</span><span class="sxs-lookup"><span data-stu-id="4191f-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="4191f-133">Onder **registratiekenmerken**, selecteert u het kenmerk **weergavenaam**.</span><span class="sxs-lookup"><span data-stu-id="4191f-133">Under **Sign-up attributes**, select the attribute **Display name**.</span></span>  <span data-ttu-id="4191f-134">U kunt ook andere kenmerken selecteren.</span><span class="sxs-lookup"><span data-stu-id="4191f-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="4191f-135">Onder **toepassingsclaims**, selecteert u de claims **weergavenaam** en **Object-ID van gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="4191f-135">Under **Application claims**, select the claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="4191f-136">U kunt ook andere claims selecteren.</span><span class="sxs-lookup"><span data-stu-id="4191f-136">You can select other claims as well.</span></span>
* <span data-ttu-id="4191f-137">Kopieert u de **naam** van elk beleid nadat u dit hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4191f-137">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="4191f-138">De beleidsnaam van uw wordt voorafgegaan door `b2c_1_` wanneer u het beleid opslaat.</span><span class="sxs-lookup"><span data-stu-id="4191f-138">Your policy name is prefixed with `b2c_1_` when you save the policy.</span></span>  <span data-ttu-id="4191f-139">U de naam van het beleid later nodig.</span><span class="sxs-lookup"><span data-stu-id="4191f-139">You need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="4191f-140">Nadat u beleidsregels hebt gemaakt, kunt u de app maken.</span><span class="sxs-lookup"><span data-stu-id="4191f-140">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="4191f-141">De voorbeeldcode downloaden</span><span class="sxs-lookup"><span data-stu-id="4191f-141">Download the sample code</span></span>
<span data-ttu-id="4191f-142">We hebben een werkende-voorbeeldtoepassing die gebruikmaakt van AppAuth met Azure AD B2C opgegeven [op GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="4191f-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="4191f-143">U kunt de code downloaden en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4191f-143">You can download the code and run it.</span></span> <span data-ttu-id="4191f-144">Voor het gebruik van uw eigen Azure AD B2C-tenant, volg de instructies in de [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="4191f-144">To use your own Azure AD B2C tenant, follow the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="4191f-145">Dit voorbeeld is gemaakt door de instructies Leesmij-bestand door de [AppAuth iOS-project op GitHub](https://github.com/openid/AppAuth-iOS).</span><span class="sxs-lookup"><span data-stu-id="4191f-145">This sample was created by following the README instructions by the [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="4191f-146">Voor meer informatie over de werking van de bibliotheek en de voorbeelden verwijzen naar de AppAuth README op GitHub.</span><span class="sxs-lookup"><span data-stu-id="4191f-146">For more details on how the sample and the library work, reference the AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="4191f-147">Uw app voor het gebruik van Azure AD B2C met AppAuth wijzigen</span><span class="sxs-lookup"><span data-stu-id="4191f-147">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="4191f-148">AppAuth biedt ondersteuning voor iOS 7 en hoger.</span><span class="sxs-lookup"><span data-stu-id="4191f-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="4191f-149">Ter ondersteuning van sociale aanmeldingen op Google, SFSafariViewController is echter vereist dat iOS 9 of hoger vereist.</span><span class="sxs-lookup"><span data-stu-id="4191f-149">However, to support social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="4191f-150">Configuratie</span><span class="sxs-lookup"><span data-stu-id="4191f-150">Configuration</span></span>

<span data-ttu-id="4191f-151">U kunt de communicatie met Azure AD B2C configureren door het eindpunt voor autorisatie en de token eindpunt URI's te geven.</span><span class="sxs-lookup"><span data-stu-id="4191f-151">You can configure communication with Azure AD B2C by specifying both the authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="4191f-152">Als deze URI's worden gegenereerd, moet u de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="4191f-152">To generate these URIs, you need the following information:</span></span>
* <span data-ttu-id="4191f-153">Tenant-ID (bijvoorbeeld: contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="4191f-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="4191f-154">De naam van beleid (bijvoorbeeld B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="4191f-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="4191f-155">Eindpunt van het token URI kan worden gegenereerd door het vervangen van de Tenant\_-ID en het beleid\_naam in de volgende URL:</span><span class="sxs-lookup"><span data-stu-id="4191f-155">The token endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="4191f-156">De autorisatie-eindpunt URI kan worden gegenereerd door het vervangen van de Tenant\_-ID en het beleid\_naam in de volgende URL:</span><span class="sxs-lookup"><span data-stu-id="4191f-156">The authorization endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="4191f-157">Voer de volgende code om uw AuthorizationServiceConfiguration-object te maken:</span><span class="sxs-lookup"><span data-stu-id="4191f-157">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready to perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="4191f-158">Autoriseren</span><span class="sxs-lookup"><span data-stu-id="4191f-158">Authorizing</span></span>

<span data-ttu-id="4191f-159">Na het configureren van of bij het ophalen van een configuratie van de service autorisatie, kan een autorisatieaanvraag worden samengesteld.</span><span class="sxs-lookup"><span data-stu-id="4191f-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="4191f-160">Voor het maken van de aanvraag, moet u de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="4191f-160">To create the request, you need the following information:</span></span>  
* <span data-ttu-id="4191f-161">Client-ID (bijvoorbeeld 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="4191f-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="4191f-162">Omleidings-URI met een aangepast schema (bijvoorbeeld com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span><span class="sxs-lookup"><span data-stu-id="4191f-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="4191f-163">Beide items moeten zijn opgeslagen als u zijn [u uw app registreert](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="4191f-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

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

<span data-ttu-id="4191f-164">Als u uw toepassing voor het afhandelen van de omleiding naar de URI met het aangepaste schema instelt, moet u de lijst met URL's in uw Info.pList bijwerken:</span><span class="sxs-lookup"><span data-stu-id="4191f-164">To set up your application to handle the redirect to the URI with the custom scheme, you need to update the list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="4191f-165">Open Info.pList.</span><span class="sxs-lookup"><span data-stu-id="4191f-165">Open Info.pList.</span></span>
* <span data-ttu-id="4191f-166">Beweeg de muisaanwijzer over een rij zoals bundel OS typecode en klik op de \+ symbool.</span><span class="sxs-lookup"><span data-stu-id="4191f-166">Hover over a row like 'Bundle OS Type Code' and click the \+ symbol.</span></span>
* <span data-ttu-id="4191f-167">Wijzig de naam van de nieuwe rij URL-typen.</span><span class="sxs-lookup"><span data-stu-id="4191f-167">Rename the new row 'URL types'.</span></span>
* <span data-ttu-id="4191f-168">Klik op de pijl naar links van de URL-types openen van de boomstructuur.</span><span class="sxs-lookup"><span data-stu-id="4191f-168">Click the arrow to the left of 'URL types' to open the tree.</span></span>
* <span data-ttu-id="4191f-169">Klik op de pijl naar links van ' 0' om te openen van de structuur-Item.</span><span class="sxs-lookup"><span data-stu-id="4191f-169">Click the arrow to the left of 'Item 0' to open the tree.</span></span>
* <span data-ttu-id="4191f-170">Wijzig de naam van eerste onderliggende Item 0 om te URL-schema-item.</span><span class="sxs-lookup"><span data-stu-id="4191f-170">Rename first item underneath Item 0 to 'URL Schemes'.</span></span>
* <span data-ttu-id="4191f-171">Klik op de pijl naar links van 'URL Schemes' te openen van de boomstructuur.</span><span class="sxs-lookup"><span data-stu-id="4191f-171">Click the arrow to the left of 'URL Schemes' to open the tree.</span></span>
* <span data-ttu-id="4191f-172">In de kolom 'Value' is een leeg veld aan de linkerkant van '0 Item' onder de URL-schema.</span><span class="sxs-lookup"><span data-stu-id="4191f-172">In the 'Value' column, there is a blank field to the left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="4191f-173">Stel de waarde voor uw unieke toepassingsschema.</span><span class="sxs-lookup"><span data-stu-id="4191f-173">Set the value to your application's unique scheme.</span></span>  <span data-ttu-id="4191f-174">De waarde moet overeenkomen met het schema in URL omleiding gebruikt bij het maken van het object OIDAuthorizationRequest.</span><span class="sxs-lookup"><span data-stu-id="4191f-174">The value must match the scheme used in redirectURL when creating the OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="4191f-175">In ons voorbeeld hebben we het schema 'com.onmicrosoft.fabrikamb2c.exampleapp' gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4191f-175">In our sample, we used the scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="4191f-176">Raadpleeg de [AppAuth handleiding](https://openid.github.io/AppAuth-iOS/) voor het voltooien van de rest van het proces.</span><span class="sxs-lookup"><span data-stu-id="4191f-176">Refer to the [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how to complete the rest of the process.</span></span> <span data-ttu-id="4191f-177">Als u snel aan de slag met een werkende app wilt, Bekijk [ons voorbeeld](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="4191f-177">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="4191f-178">Volg de stappen in de [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) invoeren van de configuratie van uw eigen Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="4191f-178">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="4191f-179">We kunnen worden altijd feedback en suggesties!</span><span class="sxs-lookup"><span data-stu-id="4191f-179">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="4191f-180">Als u problemen met dit onderwerp ondervindt of aanbevelingen voor het verbeteren van de inhoud hebben, zouden we stellen uw feedback onder aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="4191f-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="4191f-181">Voor functieaanvragen, voeg deze toe aan [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="4191f-181">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
