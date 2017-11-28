---
title: aaaAzure Active Directory v2.0 Android-app | Microsoft Docs
description: Hoe Hallo toobuild een Android-app die zich aanmeldt gebruikers met zowel persoonlijke Microsoft-account en werk of schoolaccounts en aanroepen Graph API met behulp van de bibliotheken van derden.
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 16294c07-f27d-45c9-833f-7dbb12083794
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1dd40bd3bcea28c629abce09abaed66b38774162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="aa1a6-103">Aanmelden tooan Android-app met behulp van een derde partij-bibliotheek met Graph API met behulp van Hallo v2.0-eindpunt toevoegen</span><span class="sxs-lookup"><span data-stu-id="aa1a6-103">Add sign-in tooan Android app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="aa1a6-104">Hallo Microsoft identity-platform gebruikt open standaarden, zoals OAuth2 en OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="aa1a6-105">Ontwikkelaars kunnen een bibliotheek, ze toointegrate met onze services willen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="aa1a6-106">ons platform toohelp ontwikkelaars gebruiken met andere bibliotheken, hebben we hoe de enkele scenario's zoals deze één toodemonstrate geschreven tooconfigure van derden bibliotheken tooconnect toohello Microsoft identity-platform.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="aa1a6-107">De meeste bibliotheken die implementeren [hello RFC6749 OAuth2-specificatie](https://tools.ietf.org/html/rfc6749) verbinding kunnen maken van toohello Microsoft identity-platform.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="aa1a6-108">Hallo-toepassing die in dit scenario maakt, kunnen gebruikers tootheir organisatie aanmelden en zoekt u naar zichzelf in hun organisatie met behulp van Hallo Graph API.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for themselves in their organization by using hello Graph API.</span></span>

<span data-ttu-id="aa1a6-109">Als u nieuwe tooOAuth2 of OpenID Connect, kan veel van deze voorbeeldconfiguratie zin tooyou niet maken.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="aa1a6-110">Het is raadzaam dat u leest [2.0-protocollen - stromen van OAuth 2.0 autorisatie Code](active-directory-v2-protocols-oauth-code.md) voor de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="aa1a6-111">Sommige functies van ons platform waarvoor een expressie in Hallo OAuth2 of OpenID Connect standaarden, zoals voorwaardelijke toegang en beheer van Intune vereist u toouse onze open-source bibliotheken voor Microsoft Azure identiteit.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="aa1a6-112">Hallo v2.0-eindpunt biedt geen ondersteuning voor alle Azure Active Directory-scenario's en onderdelen.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="aa1a6-113">toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="aa1a6-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-hello-code-from-github"></a><span data-ttu-id="aa1a6-114">Hallo code vanuit GitHub downloaden</span><span class="sxs-lookup"><span data-stu-id="aa1a6-114">Download hello code from GitHub</span></span>
<span data-ttu-id="aa1a6-115">Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span><span class="sxs-lookup"><span data-stu-id="aa1a6-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="aa1a6-116">toofollow langs, kunt u [basis van Hallo app downloaden als een ZIP-](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) of kloon Hallo basisproject:</span><span class="sxs-lookup"><span data-stu-id="aa1a6-116">toofollow along, you can  [download hello app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="aa1a6-117">U kunt ook gewoon Hallo voorbeeld downloaden en meteen aan de slag:</span><span class="sxs-lookup"><span data-stu-id="aa1a6-117">You can also just download hello sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="aa1a6-118">Een app registreren</span><span class="sxs-lookup"><span data-stu-id="aa1a6-118">Register an app</span></span>
<span data-ttu-id="aa1a6-119">Maak een nieuwe app op Hallo [toepassing registratieportal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of volgen gedetailleerde stappen op Hallo [hoe tooregister een app met Hallo v2.0-eindpunt](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="aa1a6-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="aa1a6-120">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="aa1a6-120">Make sure to:</span></span>

* <span data-ttu-id="aa1a6-121">Kopiëren Hallo **toepassings-Id** die is toegewezen tooyour app omdat u hebt deze snel nodig.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="aa1a6-122">Hallo toevoegen **Mobile** platform voor uw app.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-122">Add hello **Mobile** platform for your app.</span></span>

> <span data-ttu-id="aa1a6-123">Opmerking: Hallo-portal voor registratie van toepassing biedt een **omleidings-URI** waarde.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-123">Note: hello Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="aa1a6-124">In dit voorbeeld moet u de standaardwaarde Hallo van gebruiken `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-124">However, in this example you must use hello default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="aa1a6-125">Hallo NXOAuth2 van derden bibliotheek downloaden en een werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="aa1a6-125">Download hello NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="aa1a6-126">Voor dit scenario gebruikt u Hallo OIDCAndroidLib vanuit GitHub, namelijk een OAuth2-bibliotheek op basis van Hallo OpenID Connect code van Google.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-126">For this walkthrough, you will use hello OIDCAndroidLib from GitHub, which is an OAuth2 library based on hello OpenID Connect code of Google.</span></span> <span data-ttu-id="aa1a6-127">Hallo systeemeigen toepassingsprofiel implementeert en ondersteunt Hallo autorisatie endpoint van Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-127">It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="aa1a6-128">Dit zijn alles van hello, moet u toointegrate met Hallo Microsoft identiteitsplatform.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-128">These are all hello things that you'll need toointegrate with hello Microsoft identity platform.</span></span>

<span data-ttu-id="aa1a6-129">Kloon Hallo OIDCAndroidLib opslagplaats tooyour computer.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-129">Clone hello OIDCAndroidLib repo tooyour computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="aa1a6-131">Uw Android Studio-omgeving instellen</span><span class="sxs-lookup"><span data-stu-id="aa1a6-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="aa1a6-132">Maak een nieuw Android Studio-project en accepteer de standaardinstellingen Hallo in Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-132">Create a new Android Studio project and accept hello defaults in hello wizard.</span></span>
   
    ![Nieuw project in Android Studio maken](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Doel Android-apparaten](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Een activiteit toomobile toevoegen](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="aa1a6-136">tooset van uw projectmodules Hallo gekloond opslagplaats toohello projectlocatie verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-136">tooset up your project modules, move hello cloned repo toohello project location.</span></span> <span data-ttu-id="aa1a6-137">U kunt ook Hallo-project maken en te klonen rechtstreeks toohello projectlocatie.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-137">You can also create hello project and then clone it directly toohello project location.</span></span>
   
    ![Projectmodules](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="aa1a6-139">Open Hallo-projectinstellingen modules met behulp van Hallo contextmenu of met behulp van Hallo Ctrl + Alt + rimaire + S snelkoppeling.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-139">Open hello project modules settings by using hello context menu or by using hello Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![Modules projectinstellingen](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="aa1a6-141">Hallo standaard app module verwijderen omdat u wilt dat alleen Hallo container projectinstellingen.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-141">Remove hello default app module because you only want hello project container settings.</span></span>
   
    ![Hallo standaard app module](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="aa1a6-143">Modules importeren vanuit Hallo gekloonde opslagplaats toohello huidige project.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-143">Import modules from hello cloned repo toohello current project.</span></span>
   
    <span data-ttu-id="aa1a6-144">![Project importeren in gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![nieuwe modulepagina maken](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="aa1a6-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="aa1a6-145">Herhaal deze stappen voor Hallo `oidlib-sample` module.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-145">Repeat these steps for hello `oidlib-sample` module.</span></span>
7. <span data-ttu-id="aa1a6-146">Hallo oidclib afhankelijkheden op Hallo controleren `oidlib-sample` module.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-146">Check hello oidclib dependencies on hello `oidlib-sample` module.</span></span>
   
    ![oidclib afhankelijkheden op Hallo oidlib voorbeeld module](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="aa1a6-148">Klik op **OK** en wacht tot gradle synchroniseren.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="aa1a6-149">Uw settings.gradle moet eruitzien als:</span><span class="sxs-lookup"><span data-stu-id="aa1a6-149">Your settings.gradle should look like:</span></span>
   
    ![Schermopname van settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="aa1a6-151">Hallo voorbeeld-app toomake ervoor bouwen dat Hallo voorbeeld juist worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-151">Build hello sample app toomake sure that hello sample running correctly.</span></span>
   
    <span data-ttu-id="aa1a6-152">U niet kunt toouse dit met Azure Active Directory nog.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-152">You won't be able toouse this with Azure Active Directory yet.</span></span> <span data-ttu-id="aa1a6-153">Moeten we tooconfigure sommige eindpunten eerst.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-153">We'll need tooconfigure some endpoints first.</span></span> <span data-ttu-id="aa1a6-154">Dit is tooensure die u hebt geen een problemen Android Studio voordat we Hallo voorbeeld-app aanpassen.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-154">This is tooensure you don't have an Android Studio issues before we start customizing hello sample app.</span></span>
10. <span data-ttu-id="aa1a6-155">Bouwen en uitvoeren van `oidlib-sample` als doel Hallo in Android Studio.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-155">Build and run `oidlib-sample` as hello target in Android Studio.</span></span>
    
    ![Voortgang van de build oidlib-voorbeeld](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="aa1a6-157">Hallo verwijderen `app ` map die is gegeven wanneer u Hallo module verwijderd uit Hallo project omdat Android Studio niet worden verwijderd voor de veiligheid.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-157">Delete hello `app ` directory that was left when you removed hello module from hello project because Android Studio doesn't delete it for safety.</span></span>
    
    ![Bestandsstructuur met Hallo app-map](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="aa1a6-159">Open Hallo **configuraties bewerken** menu tooremove Hallo uitvoeren configuratie die ook gegeven is wanneer u Hallo module verwijderd uit het Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-159">Open hello **Edit Configurations** menu tooremove hello run configuration that was also left when you removed hello module from hello project.</span></span>
    
    <span data-ttu-id="aa1a6-160">![Configuraties menu Bewerken](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![configuratie van de app uitvoeren](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="aa1a6-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-hello-endpoints-of-hello-sample"></a><span data-ttu-id="aa1a6-161">Hallo-eindpunten van Hallo voorbeeld configureren</span><span class="sxs-lookup"><span data-stu-id="aa1a6-161">Configure hello endpoints of hello sample</span></span>
<span data-ttu-id="aa1a6-162">Nu dat u Hallo hebt `oidlib-sample` met succes is uitgevoerd, bewerk de sommige eindpunten tooget gaan we deze werken met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-162">Now that you have hello `oidlib-sample` running successfully, let's edit some endpoints tooget this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a><span data-ttu-id="aa1a6-163">Configureren van de client door Hallo oidc_clientconf.xml bestand te bewerken</span><span class="sxs-lookup"><span data-stu-id="aa1a6-163">Configure your client by editing hello oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="aa1a6-164">Omdat u van OAuth2 stromen alleen tooget een token gebruikmaakt en Hallo Graph API aanroept, stel Hallo client toodo OAuth2 alleen.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-164">Because you are using OAuth2 flows only tooget a token and call hello Graph API, set hello client toodo OAuth2 only.</span></span> <span data-ttu-id="aa1a6-165">OIDC wordt geleverd in een voorbeeld van een hoger.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="aa1a6-166">Configureer uw client-ID die u hebt ontvangen van Hallo-portal voor wachtwoordregistratie.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-166">Configure your client ID that you received from hello registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="aa1a6-167">Configureer uw omleidings-URI Hello een hieronder.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-167">Configure your redirect URI with hello one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="aa1a6-168">Configureer uw scopes die u nodig hebt in volgorde tooaccess Hallo Graph API.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-168">Configure your scopes that you need in order tooaccess hello Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="aa1a6-169">Hallo `User.Read` waarde in `oidc_scopes` kunt u tooread Hallo basisprofiel Hallo gebruiker aangemeld.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-169">hello `User.Read` value in `oidc_scopes` allows you tooread hello basic profile hello signed in user.</span></span>
<span data-ttu-id="aa1a6-170">U kunt meer informatie over alle beschikbare Hallo-scopes op [Microsoft Graph-machtigingsbereiken](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="aa1a6-170">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="aa1a6-171">Als u wilt uitleg over `openid` of `offline_access` als scopes in het OpenID Connect, Zie [2.0-protocollen - stromen van OAuth 2.0 autorisatie Code](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="aa1a6-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a><span data-ttu-id="aa1a6-172">Uw clienteindpunten configureren door Hallo oidc_endpoints.xml bestand te bewerken</span><span class="sxs-lookup"><span data-stu-id="aa1a6-172">Configure your client endpoints by editing hello oidc_endpoints.xml file</span></span>
* <span data-ttu-id="aa1a6-173">Open Hallo `oidc_endpoints.xml` en breng zo Hallo volgende wijzigingen:</span><span class="sxs-lookup"><span data-stu-id="aa1a6-173">Open hello `oidc_endpoints.xml` file and make hello following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="aa1a6-174">Deze eindpunten moeten nooit wijzigen als u OAuth2 als protocol gebruikt.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="aa1a6-175">Hallo-eindpunten voor `userInfoEndpoint` en `revocationEndpoint` worden momenteel niet ondersteund door Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-175">hello endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="aa1a6-176">Als u deze met de standaardwaarde voorbeeld.com Hallo laat, wordt u eraan herinnerd dat ze niet beschikbaar in de steekproef Hallo zijn :-)</span><span class="sxs-lookup"><span data-stu-id="aa1a6-176">If you leave these with hello default example.com value, you will be reminded that they are not available in hello sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="aa1a6-177">Configureer een Graph API-aanroep</span><span class="sxs-lookup"><span data-stu-id="aa1a6-177">Configure a Graph API call</span></span>
* <span data-ttu-id="aa1a6-178">Open Hallo `HomeActivity.java` en breng zo Hallo volgende wijzigingen:</span><span class="sxs-lookup"><span data-stu-id="aa1a6-178">Open hello `HomeActivity.java` file and make hello following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="aa1a6-179">Hier wordt een eenvoudige Graph API-aanroep onze informatie geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="aa1a6-180">Alle Hallo wijzigingen dat u toodo moet zijn.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-180">Those are all hello changes that you need toodo.</span></span> <span data-ttu-id="aa1a6-181">Voer Hallo `oidlib-sample` toepassing en klik op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-181">Run hello `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="aa1a6-182">Nadat u hebt geverifieerd, selecteert u Hallo **een beveiligde bron aanvragen** knop tootest uw aanroep toohello Graph API.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-182">After you've successfully authenticated, select hello **Request Protected Resource** button tootest your call toohello Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="aa1a6-183">Beveiligingsupdates voor onze product</span><span class="sxs-lookup"><span data-stu-id="aa1a6-183">Get security updates for our product</span></span>
<span data-ttu-id="aa1a6-184">We raden u tooget meldingen over beveiligingsincidenten via Hallo [Security TechCenter](https://technet.microsoft.com/security/dd252948) en u te abonneren tooSecurity Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="aa1a6-184">We encourage you tooget notifications about security incidents by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

