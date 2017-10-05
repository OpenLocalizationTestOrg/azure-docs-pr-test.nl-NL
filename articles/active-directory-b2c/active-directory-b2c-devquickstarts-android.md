---
title: 'Azure Active Directory B2C: Ophalen van een token met behulp van een Android-toepassing | Microsoft Docs'
description: "In dit artikel wordt beschreven hoe u een Android-app die gebruikmaakt van AppAuth met Azure Active Directory B2C gebruikersidentiteiten te beheren en verifiëren van gebruikers te maken."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: d00947c3-dcaa-4cb3-8c2e-d94e0746d8b2
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 03/06/2017
ms.author: parakhj
ms.openlocfilehash: cd4b8048245be49ea79bcb1b364f2f99c56f8291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="70d59-103">Azure AD B2C: Meld u aan met een Android-toepassing</span><span class="sxs-lookup"><span data-stu-id="70d59-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="70d59-104">Op het Microsoft Identity-platform wordt gebruikgemaakt van open standaarden, zoals OAuth2 en OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="70d59-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="70d59-105">Ontwikkelaars kunnen daardoor gebruikmaken van elke gewenste bibliotheek die ze met onze services willen integreren.</span><span class="sxs-lookup"><span data-stu-id="70d59-105">This allows developers to leverage any library they wish to integrate with our services.</span></span> <span data-ttu-id="70d59-106">Om ontwikkelaars bij het gebruik van ons platform met andere bibliotheken, geschreven we enkele scenario's zoals deze te laten zien hoe 3e partij mediawisselaars verbinding maken met het identiteitsplatform van Microsoft te configureren.</span><span class="sxs-lookup"><span data-stu-id="70d59-106">To aid developers in using our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure 3rd party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="70d59-107">De meeste bibliotheken die de [OAuth2-specificatie RFC6749](https://tools.ietf.org/html/rfc6749) implementeren, kunnen verbinding maken met het Microsoft Identity-platform.</span><span class="sxs-lookup"><span data-stu-id="70d59-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="70d59-108">Microsoft biedt geen oplossingen voor 3rd partij bibliotheken en een overzicht van deze bibliotheken niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="70d59-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="70d59-109">Dit voorbeeld maakt gebruik van een 3e partij-bibliotheek AppAuth dat is getest op compatibiliteit in algemene scenario's met de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="70d59-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="70d59-110">Problemen en functie-aanvragen moeten worden omgeleid naar de bibliotheek open source-project.</span><span class="sxs-lookup"><span data-stu-id="70d59-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="70d59-111">Zie [in dit artikel](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="70d59-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="70d59-112">Als u nog geen ervaring hebt met OAuth2 of OpenID Connect, zal een groot gedeelte van deze voorbeeldconfiguratie u niet veel zeggen.</span><span class="sxs-lookup"><span data-stu-id="70d59-112">If you're new to OAuth2 or OpenID Connect much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="70d59-113">U wordt geadviseerd eerst een beknopt [overzicht van het hier gedocumenteerde protocol te bekijken](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="70d59-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="70d59-114">Een Azure AD B2C-directory maken</span><span class="sxs-lookup"><span data-stu-id="70d59-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="70d59-115">Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken.</span><span class="sxs-lookup"><span data-stu-id="70d59-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="70d59-116">Een directory is een container voor alle gebruikers, apps, groepen en meer.</span><span class="sxs-lookup"><span data-stu-id="70d59-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="70d59-117">Als u nog geen directory hebt, [maakt u een B2C-directory](active-directory-b2c-get-started.md) voordat u verdergaat.</span><span class="sxs-lookup"><span data-stu-id="70d59-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="70d59-118">Een app maken</span><span class="sxs-lookup"><span data-stu-id="70d59-118">Create an application</span></span>

<span data-ttu-id="70d59-119">Vervolgens maakt u een app in uw B2C-directory.</span><span class="sxs-lookup"><span data-stu-id="70d59-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="70d59-120">Hiermee geeft u informatie door aan Azure AD die nodig is om veilig te communiceren met uw app.</span><span class="sxs-lookup"><span data-stu-id="70d59-120">This gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="70d59-121">Volg voor het maken van een mobiele app [deze instructies](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="70d59-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="70d59-122">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="70d59-122">Be sure to:</span></span>

* <span data-ttu-id="70d59-123">Omvatten een **Native Client** in de toepassing.</span><span class="sxs-lookup"><span data-stu-id="70d59-123">Include a **Native Client** in the application.</span></span>
* <span data-ttu-id="70d59-124">U de **toepassings-id** kopieert die is toegewezen aan uw app.</span><span class="sxs-lookup"><span data-stu-id="70d59-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="70d59-125">U nodig deze later.</span><span class="sxs-lookup"><span data-stu-id="70d59-125">You will need this later.</span></span>
* <span data-ttu-id="70d59-126">Instellen van een native client **omleidings-URI** (bijvoorbeeld com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="70d59-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="70d59-127">Deze hebt u ook later nodig.</span><span class="sxs-lookup"><span data-stu-id="70d59-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="70d59-128">Het beleid maken</span><span class="sxs-lookup"><span data-stu-id="70d59-128">Create your policies</span></span>

<span data-ttu-id="70d59-129">In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="70d59-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="70d59-130">Deze app bevat één identiteit ervaring: een gecombineerde aanmelden en registreren.</span><span class="sxs-lookup"><span data-stu-id="70d59-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="70d59-131">U moet maken dit beleid, zoals beschreven in de [naslagartikel](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="70d59-131">You need to create this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="70d59-132">Wanneer u het beleid maakt:</span><span class="sxs-lookup"><span data-stu-id="70d59-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="70d59-133">Kies de **weergavenaam** als een kenmerk aanmelding in uw beleid.</span><span class="sxs-lookup"><span data-stu-id="70d59-133">Choose the **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="70d59-134">Kiest u **Weergavenaam**- en **Object-id**-toepassingsclaims voor elk beleid.</span><span class="sxs-lookup"><span data-stu-id="70d59-134">Choose the **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="70d59-135">U kunt ook andere claims kiezen.</span><span class="sxs-lookup"><span data-stu-id="70d59-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="70d59-136">Kopieert u de **naam** van elk beleid nadat u dit hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="70d59-136">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="70d59-137">Deze moet het voorvoegsel `b2c_1_` bevatten.</span><span class="sxs-lookup"><span data-stu-id="70d59-137">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="70d59-138">U hebt de beleidsnaam later nodig.</span><span class="sxs-lookup"><span data-stu-id="70d59-138">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="70d59-139">Nadat u beleidsregels hebt gemaakt, kunt u de app maken.</span><span class="sxs-lookup"><span data-stu-id="70d59-139">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="70d59-140">De voorbeeldcode downloaden</span><span class="sxs-lookup"><span data-stu-id="70d59-140">Download the sample code</span></span>

<span data-ttu-id="70d59-141">We hebben een werkende-voorbeeldtoepassing die gebruikmaakt van AppAuth met Azure AD B2C opgegeven [op GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="70d59-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="70d59-142">U kunt de code downloaden en uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="70d59-142">You can download the code and run it.</span></span> <span data-ttu-id="70d59-143">U kunt snel aan de slag met uw eigen app met behulp van uw eigen Azure AD B2C-configuratie door de instructies in de [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="70d59-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="70d59-144">Het voorbeeld is een wijziging van het voorbeeld dat is opgegeven door [AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="70d59-144">The sample is a modification of the sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="70d59-145">Ga naar de pagina voor meer informatie over AppAuth en de bijbehorende functies.</span><span class="sxs-lookup"><span data-stu-id="70d59-145">Please visit their page to learn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="70d59-146">Uw app voor het gebruik van Azure AD B2C met AppAuth wijzigen</span><span class="sxs-lookup"><span data-stu-id="70d59-146">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="70d59-147">AppAuth biedt ondersteuning voor Android-API 16 (Jellybean) en hoger.</span><span class="sxs-lookup"><span data-stu-id="70d59-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="70d59-148">Het is raadzaam met behulp van API 23 en hoger.</span><span class="sxs-lookup"><span data-stu-id="70d59-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="70d59-149">Configuratie</span><span class="sxs-lookup"><span data-stu-id="70d59-149">Configuration</span></span>

<span data-ttu-id="70d59-150">U kunt de communicatie met Azure AD B2C configureren door de URI van de detectie of door het eindpunt voor autorisatie en de token eindpunt URI's te geven.</span><span class="sxs-lookup"><span data-stu-id="70d59-150">You can configure communication with Azure AD B2C by either specifying the discovery URI or by specifying both the authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="70d59-151">In beide gevallen moet u de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="70d59-151">In either case, you will need the following information:</span></span>

* <span data-ttu-id="70d59-152">Tenant-ID (bijvoorbeeld contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="70d59-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="70d59-153">De naam van beleid (bijvoorbeeld B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="70d59-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="70d59-154">Als u kiest voor het automatisch detecteren van de autorisatie en -tokeneindpunt URI's, moet u informatie ophalen van de URI van de detectie.</span><span class="sxs-lookup"><span data-stu-id="70d59-154">If you choose to automatically discover the authorization and token endpoint URIs, you will need to fetch information from the discovery URI.</span></span> <span data-ttu-id="70d59-155">Detectie van de URI kan worden gegenereerd door het vervangen van de Tenant\_-ID en het beleid\_naam in de volgende URL:</span><span class="sxs-lookup"><span data-stu-id="70d59-155">The discovery URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="70d59-156">U kunt de autorisatie- en eindpunt URI's van de token verkrijgen en een AuthorizationServiceConfiguration-object maken door het volgende:</span><span class="sxs-lookup"><span data-stu-id="70d59-156">You can then acquire the authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running the following:</span></span>

```java
final Uri issuerUri = Uri.parse(mDiscoveryURI);
AuthorizationServiceConfiguration config;

AuthorizationServiceConfiguration.fetchFromIssuer(
    issuerUri,
    new RetrieveConfigurationCallback() {
      @Override public void onFetchConfigurationCompleted(
          @Nullable AuthorizationServiceConfiguration serviceConfiguration,
          @Nullable AuthorizationException ex) {
        if (ex != null) {
            Log.w(TAG, "Failed to retrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed to authorization...
        }
      }
  });
```

<span data-ttu-id="70d59-157">In plaats van detectie voor informatie over de autorisatie en -tokeneindpunt URI's, kunt u ook opgeven ze expliciet door het vervangen van de Tenant\_-ID en het beleid\_hieronder de naam in de URL:</span><span class="sxs-lookup"><span data-stu-id="70d59-157">Instead of using discovery to obtain the authorization and token endpoint URIs, you can also specify them explicitly by replacing the Tenant\_ID and the Policy\_Name in the URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="70d59-158">Voer de volgende code om uw AuthorizationServiceConfiguration-object te maken:</span><span class="sxs-lookup"><span data-stu-id="70d59-158">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="70d59-159">Autoriseren</span><span class="sxs-lookup"><span data-stu-id="70d59-159">Authorizing</span></span>

<span data-ttu-id="70d59-160">Na het configureren van of bij het ophalen van een configuratie van de service autorisatie, kan een autorisatieaanvraag worden samengesteld.</span><span class="sxs-lookup"><span data-stu-id="70d59-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="70d59-161">Voor het maken van de aanvraag, moet u de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="70d59-161">To create the request, you will need the following information:</span></span>

* <span data-ttu-id="70d59-162">Client-ID (bijvoorbeeld 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="70d59-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="70d59-163">Omleidings-URI met een aangepast schema (bijvoorbeeld com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span><span class="sxs-lookup"><span data-stu-id="70d59-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="70d59-164">Beide items moeten zijn opgeslagen als u zijn [u uw app registreert](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="70d59-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="70d59-165">Raadpleeg de [AppAuth handleiding](https://openid.github.io/AppAuth-Android/) voor het voltooien van de rest van het proces.</span><span class="sxs-lookup"><span data-stu-id="70d59-165">Please refer to the [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how to complete the rest of the process.</span></span> <span data-ttu-id="70d59-166">Als u snel aan de slag met een werkende app wilt, Bekijk [ons voorbeeld](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="70d59-166">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="70d59-167">Volg de stappen in de [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) invoeren van de configuratie van uw eigen Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="70d59-167">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="70d59-168">We kunnen worden altijd feedback en suggesties!</span><span class="sxs-lookup"><span data-stu-id="70d59-168">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="70d59-169">Als u problemen met dit onderwerp ondervindt of aanbevelingen voor het verbeteren van de inhoud hebben, zouden we stellen uw feedback onder aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="70d59-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="70d59-170">Voor functieaanvragen, voeg deze toe aan [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="70d59-170">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

