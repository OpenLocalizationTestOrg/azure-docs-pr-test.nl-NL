---
title: 'Azure Active Directory B2C: Ophalen van een token met behulp van een Android-toepassing | Microsoft Docs'
description: "In dit artikel wordt uitgelegd hoe u toocreate een Android-app die gebruikmaakt van AppAuth met Azure Active Directory B2C toomanage gebruikers-id's en gebruikers te verifiëren."
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
ms.openlocfilehash: 0236398673115a34951f035cb1e73e89417abf86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="13bf4-103">Azure AD B2C: Meld u aan met een Android-toepassing</span><span class="sxs-lookup"><span data-stu-id="13bf4-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="13bf4-104">Hallo Microsoft identity-platform gebruikt open standaarden, zoals OAuth2 en OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="13bf4-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="13bf4-105">Hierdoor kunnen ontwikkelaars tooleverage een bibliotheek, willen ze toointegrate met onze services.</span><span class="sxs-lookup"><span data-stu-id="13bf4-105">This allows developers tooleverage any library they wish toointegrate with our services.</span></span> <span data-ttu-id="13bf4-106">tooaid ontwikkelaars bij het gebruik van ons platform met andere bibliotheken, we geschreven enkele scenario's zoals deze één toodemonstrate hoe tooconfigure 3e partij bibliotheken tooconnect toohello Microsoft identity-platform.</span><span class="sxs-lookup"><span data-stu-id="13bf4-106">tooaid developers in using our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure 3rd party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="13bf4-107">De meeste bibliotheken die implementeren [hello RFC6749 OAuth2-specificatie](https://tools.ietf.org/html/rfc6749) worden kunnen tooconnect toohello Microsoft Identity-platform.</span><span class="sxs-lookup"><span data-stu-id="13bf4-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="13bf4-108">Microsoft biedt geen oplossingen voor 3rd partij bibliotheken en een overzicht van deze bibliotheken niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="13bf4-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="13bf4-109">Dit voorbeeld maakt gebruik van een 3e partij-bibliotheek AppAuth dat is getest op compatibiliteit in algemene scenario's met hello Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="13bf4-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="13bf4-110">Problemen en functie-aanvragen moeten gerichte toohello-bibliotheek open source-project.</span><span class="sxs-lookup"><span data-stu-id="13bf4-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="13bf4-111">Zie [in dit artikel](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="13bf4-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="13bf4-112">Als u nieuwe tooOAuth2 of OpenID Connect mogelijk veel van deze voorbeeldconfiguratie veel tooyou zin niet maken.</span><span class="sxs-lookup"><span data-stu-id="13bf4-112">If you're new tooOAuth2 or OpenID Connect much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="13bf4-113">We raden u een korte bekijkt [overzicht van het Hallo-protocol we hier hebt gedocumenteerd](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="13bf4-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="13bf4-114">Een Azure AD B2C-directory maken</span><span class="sxs-lookup"><span data-stu-id="13bf4-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="13bf4-115">Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken.</span><span class="sxs-lookup"><span data-stu-id="13bf4-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="13bf4-116">Een directory is een container voor alle gebruikers, apps, groepen en meer.</span><span class="sxs-lookup"><span data-stu-id="13bf4-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="13bf4-117">Als u nog geen directory hebt, [maakt u een B2C-directory](active-directory-b2c-get-started.md) voordat u verdergaat.</span><span class="sxs-lookup"><span data-stu-id="13bf4-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="13bf4-118">Een app maken</span><span class="sxs-lookup"><span data-stu-id="13bf4-118">Create an application</span></span>

<span data-ttu-id="13bf4-119">Vervolgens moet u een app toocreate in uw B2C-directory.</span><span class="sxs-lookup"><span data-stu-id="13bf4-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="13bf4-120">Hiermee geeft u Azure AD-informatie dat het moet toocommunicate veilig met uw app.</span><span class="sxs-lookup"><span data-stu-id="13bf4-120">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="13bf4-121">Volg toocreate een mobiele app [deze instructies](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="13bf4-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="13bf4-122">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="13bf4-122">Be sure to:</span></span>

* <span data-ttu-id="13bf4-123">Omvatten een **Native Client** in Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="13bf4-123">Include a **Native Client** in hello application.</span></span>
* <span data-ttu-id="13bf4-124">Kopiëren Hallo **toepassings-ID** is toegewezen tooyour app.</span><span class="sxs-lookup"><span data-stu-id="13bf4-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="13bf4-125">U nodig deze later.</span><span class="sxs-lookup"><span data-stu-id="13bf4-125">You will need this later.</span></span>
* <span data-ttu-id="13bf4-126">Instellen van een native client **omleidings-URI** (bijvoorbeeld com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="13bf4-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="13bf4-127">Deze hebt u ook later nodig.</span><span class="sxs-lookup"><span data-stu-id="13bf4-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="13bf4-128">Het beleid maken</span><span class="sxs-lookup"><span data-stu-id="13bf4-128">Create your policies</span></span>

<span data-ttu-id="13bf4-129">In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="13bf4-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="13bf4-130">Deze app bevat één identiteit ervaring: een gecombineerde aanmelden en registreren.</span><span class="sxs-lookup"><span data-stu-id="13bf4-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="13bf4-131">U moet toocreate dit beleid, zoals beschreven in de [naslagartikel](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="13bf4-131">You need toocreate this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="13bf4-132">Wanneer u Hallo beleid maakt, moet u:</span><span class="sxs-lookup"><span data-stu-id="13bf4-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="13bf4-133">Kies Hallo **weergavenaam** als een kenmerk aanmelding in uw beleid.</span><span class="sxs-lookup"><span data-stu-id="13bf4-133">Choose hello **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="13bf4-134">Kies Hallo **weergavenaam** en **Object-ID** toepassingsclaims voor elk beleid.</span><span class="sxs-lookup"><span data-stu-id="13bf4-134">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="13bf4-135">U kunt ook andere claims kiezen.</span><span class="sxs-lookup"><span data-stu-id="13bf4-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="13bf4-136">Kopiëren Hallo **naam** van elk beleid nadat u dit hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="13bf4-136">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="13bf4-137">Het voorvoegsel Hallo heeft `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="13bf4-137">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="13bf4-138">U hebt de beleidsnaam hello later nodig.</span><span class="sxs-lookup"><span data-stu-id="13bf4-138">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="13bf4-139">Wanneer u uw beleid hebt gemaakt, bent u klaar toobuild uw app.</span><span class="sxs-lookup"><span data-stu-id="13bf4-139">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="13bf4-140">Hallo voorbeeldcode downloaden</span><span class="sxs-lookup"><span data-stu-id="13bf4-140">Download hello sample code</span></span>

<span data-ttu-id="13bf4-141">We hebben een werkende-voorbeeldtoepassing die gebruikmaakt van AppAuth met Azure AD B2C opgegeven [op GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="13bf4-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="13bf4-142">U kunt downloaden Hallo code en voer deze uit.</span><span class="sxs-lookup"><span data-stu-id="13bf4-142">You can download hello code and run it.</span></span> <span data-ttu-id="13bf4-143">U kunt snel aan de slag met uw eigen app met behulp van uw eigen Azure AD B2C-configuratie door de instructies te volgen Hallo in Hallo [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="13bf4-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="13bf4-144">Hallo-voorbeeld is een wijziging van Hallo voorbeeld dat is opgegeven door [AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="13bf4-144">hello sample is a modification of hello sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="13bf4-145">Ga naar de pagina toolearn meer over AppAuth en de bijbehorende functies.</span><span class="sxs-lookup"><span data-stu-id="13bf4-145">Please visit their page toolearn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="13bf4-146">Uw app toouse Azure AD B2C met AppAuth wijzigen</span><span class="sxs-lookup"><span data-stu-id="13bf4-146">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="13bf4-147">AppAuth biedt ondersteuning voor Android-API 16 (Jellybean) en hoger.</span><span class="sxs-lookup"><span data-stu-id="13bf4-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="13bf4-148">Het is raadzaam met behulp van API 23 en hoger.</span><span class="sxs-lookup"><span data-stu-id="13bf4-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="13bf4-149">Configuratie</span><span class="sxs-lookup"><span data-stu-id="13bf4-149">Configuration</span></span>

<span data-ttu-id="13bf4-150">U kunt de communicatie met Azure AD B2C configureren waarmee Hallo detecteren URI of door te geven zowel Hallo autorisatie eindpunt en token eindpunt URI's.</span><span class="sxs-lookup"><span data-stu-id="13bf4-150">You can configure communication with Azure AD B2C by either specifying hello discovery URI or by specifying both hello authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="13bf4-151">In beide gevallen moet u Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="13bf4-151">In either case, you will need hello following information:</span></span>

* <span data-ttu-id="13bf4-152">Tenant-ID (bijvoorbeeld contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="13bf4-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="13bf4-153">De naam van beleid (bijvoorbeeld B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="13bf4-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="13bf4-154">Als u ervoor kiezen tooautomatically Hallo autorisatie en token-eindpunt URI's detecteren, moet u toofetch informatie van Hallo detectie URI.</span><span class="sxs-lookup"><span data-stu-id="13bf4-154">If you choose tooautomatically discover hello authorization and token endpoint URIs, you will need toofetch information from hello discovery URI.</span></span> <span data-ttu-id="13bf4-155">Hallo detectie URI kan worden gegenereerd door de Hallo Tenant\_-ID en het Hallo beleid\_naam in Hallo URL te volgen:</span><span class="sxs-lookup"><span data-stu-id="13bf4-155">hello discovery URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="13bf4-156">U kunt verkrijgen Hallo autorisatie en -tokeneindpunt URI's en maken van een object AuthorizationServiceConfiguration door Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="13bf4-156">You can then acquire hello authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running hello following:</span></span>

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
            Log.w(TAG, "Failed tooretrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed tooauthorization...
        }
      }
  });
```

<span data-ttu-id="13bf4-157">In plaats van detectie tooobtain Hallo autorisatie en -tokeneindpunt URI's gebruikt, kunt u ook opgeven ze expliciet door te vervangen Hallo Tenant\_-ID en het Hallo beleid\_hieronder de naam in Hallo-URL:</span><span class="sxs-lookup"><span data-stu-id="13bf4-157">Instead of using discovery tooobtain hello authorization and token endpoint URIs, you can also specify them explicitly by replacing hello Tenant\_ID and hello Policy\_Name in hello URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="13bf4-158">Voer Hallo code toocreate na uw AuthorizationServiceConfiguration-object:</span><span class="sxs-lookup"><span data-stu-id="13bf4-158">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="13bf4-159">Autoriseren</span><span class="sxs-lookup"><span data-stu-id="13bf4-159">Authorizing</span></span>

<span data-ttu-id="13bf4-160">Na het configureren van of bij het ophalen van een configuratie van de service autorisatie, kan een autorisatieaanvraag worden samengesteld.</span><span class="sxs-lookup"><span data-stu-id="13bf4-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="13bf4-161">Hallo toocreate aanvragen, moet u Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="13bf4-161">toocreate hello request, you will need hello following information:</span></span>

* <span data-ttu-id="13bf4-162">Client-ID (bijvoorbeeld 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="13bf4-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="13bf4-163">Omleidings-URI met een aangepast schema (bijvoorbeeld com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span><span class="sxs-lookup"><span data-stu-id="13bf4-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="13bf4-164">Beide items moeten zijn opgeslagen als u zijn [u uw app registreert](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="13bf4-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="13bf4-165">Raadpleeg toohello [AppAuth handleiding](https://openid.github.io/AppAuth-Android/) op hoe toocomplete Hallo rest van het Hallo-proces.</span><span class="sxs-lookup"><span data-stu-id="13bf4-165">Please refer toohello [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="13bf4-166">Als u tooquickly moet aan de slag met een app werken, Bekijk [ons voorbeeld](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="13bf4-166">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="13bf4-167">Volg de stappen Hallo in Hallo [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter uw eigen Azure AD B2C-configuratie.</span><span class="sxs-lookup"><span data-stu-id="13bf4-167">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="13bf4-168">We zijn altijd open toofeedback en suggesties!</span><span class="sxs-lookup"><span data-stu-id="13bf4-168">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="13bf4-169">Als u problemen met dit onderwerp ondervindt of aanbevelingen voor het verbeteren van de inhoud hebben, zou wij stellen uw feedback Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="13bf4-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="13bf4-170">Voor functieaanvragen, toe te voegen te[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="13bf4-170">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

