---
title: Azure Active Directory v2.0 Android-app | Microsoft Docs
description: Het bouwen van een Android-app die gebruikers met zowel persoonlijke Microsoft-account en werk of schoolaccounts en de Graph API-aanroepen worden aangemeld met behulp van de bibliotheken van derden.
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
ms.openlocfilehash: c0a5a818c61f7af7ff04bf890b54e8364f3b21b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-android-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="38e70-103">Aanmelden toevoegen aan een Android-app met behulp van een derde partij-bibliotheek met Graph API met behulp van het v2.0-eindpunt</span><span class="sxs-lookup"><span data-stu-id="38e70-103">Add sign-in to an Android app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="38e70-104">Op het Microsoft Identity-platform wordt gebruikgemaakt van open standaarden, zoals OAuth2 en OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="38e70-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="38e70-105">Ontwikkelaars kunnen een bibliotheek die ze willen integreren in onze services gebruiken.</span><span class="sxs-lookup"><span data-stu-id="38e70-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="38e70-106">Om te helpen ons platform gebruiken met andere bibliotheken ontwikkelaars, hebben we enkele scenario's zoals deze voorbeelden van het configureren van derden bibliotheken verbinding maken met het identiteitsplatform van Microsoft geschreven.</span><span class="sxs-lookup"><span data-stu-id="38e70-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="38e70-107">De meeste bibliotheken die implementeren [de RFC6749 OAuth2-specificatie](https://tools.ietf.org/html/rfc6749) verbinding kunnen maken met het identiteitsplatform van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="38e70-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="38e70-108">Met de toepassing die in dit scenario maakt, kunnen gebruikers zich aanmelden bij hun organisatie en zoekt u naar zichzelf in hun organisatie met behulp van de Graph API.</span><span class="sxs-lookup"><span data-stu-id="38e70-108">With the application that this walkthrough creates, users can sign in to their organization and then search for themselves in their organization by using the Graph API.</span></span>

<span data-ttu-id="38e70-109">Als u geen ervaring met OAuth2 of OpenID Connect, wellicht veel van de configuratie van deze niet verstandig aan u.</span><span class="sxs-lookup"><span data-stu-id="38e70-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="38e70-110">Het is raadzaam dat u leest [2.0-protocollen - stromen van OAuth 2.0 autorisatie Code](active-directory-v2-protocols-oauth-code.md) voor de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="38e70-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="38e70-111">Sommige functies van ons platform die u een expressie in de OAuth2 of OpenID Connect standaarden, zoals voorwaardelijke toegang en beheer van Intune-beleid hebt, moeten u onze open-source bibliotheken voor Microsoft Azure identiteit gebruiken.</span><span class="sxs-lookup"><span data-stu-id="38e70-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="38e70-112">Het v2.0-eindpunt biedt geen ondersteuning voor alle Azure Active Directory-scenario's en onderdelen.</span><span class="sxs-lookup"><span data-stu-id="38e70-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="38e70-113">Meer informatie over om te bepalen of moet u het v2.0-eindpunt, [v2.0 beperkingen](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="38e70-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-the-code-from-github"></a><span data-ttu-id="38e70-114">De code van GitHub downloaden</span><span class="sxs-lookup"><span data-stu-id="38e70-114">Download the code from GitHub</span></span>
<span data-ttu-id="38e70-115">De code voor deze zelfstudie wordt onderhouden in [GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span><span class="sxs-lookup"><span data-stu-id="38e70-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="38e70-116">Als u wilt volgen, kunt u [basis van de app downloaden als een ZIP-](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) of het geraamte:</span><span class="sxs-lookup"><span data-stu-id="38e70-116">To follow along, you can  [download the app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="38e70-117">U kunt ook het voorbeeld downloaden en meteen aan de slag:</span><span class="sxs-lookup"><span data-stu-id="38e70-117">You can also just download the sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="38e70-118">Een app registreren</span><span class="sxs-lookup"><span data-stu-id="38e70-118">Register an app</span></span>
<span data-ttu-id="38e70-119">Maakt een nieuwe app op de [toepassing registratieportal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of de gedetailleerde stappen op [het registreren van een app met het v2.0-eindpunt](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="38e70-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="38e70-120">Zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="38e70-120">Make sure to:</span></span>

* <span data-ttu-id="38e70-121">Kopieer de **toepassings-Id** die toegewezen aan uw app, omdat u hebt deze snel nodig.</span><span class="sxs-lookup"><span data-stu-id="38e70-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="38e70-122">Voeg de **Mobile** platform voor uw app.</span><span class="sxs-lookup"><span data-stu-id="38e70-122">Add the **Mobile** platform for your app.</span></span>

> <span data-ttu-id="38e70-123">Opmerking: De registratieportal toepassing biedt een **omleidings-URI** waarde.</span><span class="sxs-lookup"><span data-stu-id="38e70-123">Note: The Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="38e70-124">In dit voorbeeld moet u de standaardwaarde van gebruiken `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span><span class="sxs-lookup"><span data-stu-id="38e70-124">However, in this example you must use the default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-the-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="38e70-125">De derde partij NXOAuth2 bibliotheek downloaden en een werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="38e70-125">Download the NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="38e70-126">Voor dit scenario gebruikt u de OIDCAndroidLib vanuit GitHub, namelijk een OAuth2-bibliotheek op basis van de code OpenID Connect van Google.</span><span class="sxs-lookup"><span data-stu-id="38e70-126">For this walkthrough, you will use the OIDCAndroidLib from GitHub, which is an OAuth2 library based on the OpenID Connect code of Google.</span></span> <span data-ttu-id="38e70-127">Het systeemeigen toepassingsprofiel implementeert en biedt ondersteuning voor het eindpunt voor autorisatie van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="38e70-127">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="38e70-128">Dit zijn de dingen die u wilt integreren met het identiteitsplatform van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="38e70-128">These are all the things that you'll need to integrate with the Microsoft identity platform.</span></span>

<span data-ttu-id="38e70-129">Kloon de opslagplaats OIDCAndroidLib op uw computer.</span><span class="sxs-lookup"><span data-stu-id="38e70-129">Clone the OIDCAndroidLib repo to your computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="38e70-131">Uw Android Studio-omgeving instellen</span><span class="sxs-lookup"><span data-stu-id="38e70-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="38e70-132">Maak een nieuw Android Studio-project en accepteer de standaardinstellingen in de wizard.</span><span class="sxs-lookup"><span data-stu-id="38e70-132">Create a new Android Studio project and accept the defaults in the wizard.</span></span>
   
    ![Nieuw project in Android Studio maken](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Doel Android-apparaten](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Een activiteit aan mobile toevoegen](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="38e70-136">Verplaats de gekloonde opslagplaats naar de projectlocatie voordat u uw projectmodules kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="38e70-136">To set up your project modules, move the cloned repo to the project location.</span></span> <span data-ttu-id="38e70-137">U kunt ook het project te maken en te klonen rechtstreeks naar de locatie van het project.</span><span class="sxs-lookup"><span data-stu-id="38e70-137">You can also create the project and then clone it directly to the project location.</span></span>
   
    ![Projectmodules](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="38e70-139">Open de projectinstellingen modules met behulp van het contextmenu of met behulp van de sneltoets Ctrl + Alt + rimaire + S.</span><span class="sxs-lookup"><span data-stu-id="38e70-139">Open the project modules settings by using the context menu or by using the Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![Modules projectinstellingen](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="38e70-141">De standaard app-module niet verwijderen omdat u wilt dat alleen de instellingen van de container project.</span><span class="sxs-lookup"><span data-stu-id="38e70-141">Remove the default app module because you only want the project container settings.</span></span>
   
    ![De standaard app-module](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="38e70-143">Modules importeren uit de gekloonde opslagplaats op het huidige project.</span><span class="sxs-lookup"><span data-stu-id="38e70-143">Import modules from the cloned repo to the current project.</span></span>
   
    <span data-ttu-id="38e70-144">![Project importeren in gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![nieuwe modulepagina maken](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="38e70-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="38e70-145">Herhaal deze stappen voor het `oidlib-sample` module.</span><span class="sxs-lookup"><span data-stu-id="38e70-145">Repeat these steps for the `oidlib-sample` module.</span></span>
7. <span data-ttu-id="38e70-146">De afhankelijkheden oidclib controleren op de `oidlib-sample` module.</span><span class="sxs-lookup"><span data-stu-id="38e70-146">Check the oidclib dependencies on the `oidlib-sample` module.</span></span>
   
    ![oidclib afhankelijkheden van de module oidlib-voorbeeld](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="38e70-148">Klik op **OK** en wacht tot gradle synchroniseren.</span><span class="sxs-lookup"><span data-stu-id="38e70-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="38e70-149">Uw settings.gradle moet eruitzien als:</span><span class="sxs-lookup"><span data-stu-id="38e70-149">Your settings.gradle should look like:</span></span>
   
    ![Schermopname van settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="38e70-151">Maken van de voorbeeld-app om ervoor te zorgen dat het voorbeeld juist worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="38e70-151">Build the sample app to make sure that the sample running correctly.</span></span>
   
    <span data-ttu-id="38e70-152">Het niet mogelijk nog gebruiken met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="38e70-152">You won't be able to use this with Azure Active Directory yet.</span></span> <span data-ttu-id="38e70-153">Er moet eerst een aantal eindpunten configureren.</span><span class="sxs-lookup"><span data-stu-id="38e70-153">We'll need to configure some endpoints first.</span></span> <span data-ttu-id="38e70-154">Dit is om te controleren of er geen problemen met een Android Studio laten we beginnen met het aanpassen van de voorbeeld-app.</span><span class="sxs-lookup"><span data-stu-id="38e70-154">This is to ensure you don't have an Android Studio issues before we start customizing the sample app.</span></span>
10. <span data-ttu-id="38e70-155">Bouwen en uitvoeren van `oidlib-sample` als het doel in Android Studio.</span><span class="sxs-lookup"><span data-stu-id="38e70-155">Build and run `oidlib-sample` as the target in Android Studio.</span></span>
    
    ![Voortgang van de build oidlib-voorbeeld](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="38e70-157">Verwijder de `app ` map die is gegeven wanneer u de module verwijderd uit het project omdat Android Studio niet worden verwijderd voor de veiligheid.</span><span class="sxs-lookup"><span data-stu-id="38e70-157">Delete the `app ` directory that was left when you removed the module from the project because Android Studio doesn't delete it for safety.</span></span>
    
    ![Structuur van een bestand met de app-map](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="38e70-159">Open de **configuraties bewerken** menu te verwijderen van de configuratie van de uitvoeren die ook is gegeven wanneer u de module verwijderd uit het project.</span><span class="sxs-lookup"><span data-stu-id="38e70-159">Open the **Edit Configurations** menu to remove the run configuration that was also left when you removed the module from the project.</span></span>
    
    <span data-ttu-id="38e70-160">![Configuraties menu Bewerken](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![configuratie van de app uitvoeren](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="38e70-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-the-endpoints-of-the-sample"></a><span data-ttu-id="38e70-161">De eindpunten van het voorbeeld configureren</span><span class="sxs-lookup"><span data-stu-id="38e70-161">Configure the endpoints of the sample</span></span>
<span data-ttu-id="38e70-162">Nu dat u hebt de `oidlib-sample` met succes is uitgevoerd, gaan we sommige eindpunten om deze te kunnen gebruiken met Azure Active Directory bewerken.</span><span class="sxs-lookup"><span data-stu-id="38e70-162">Now that you have the `oidlib-sample` running successfully, let's edit some endpoints to get this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-the-oidcclientconfxml-file"></a><span data-ttu-id="38e70-163">Clientcomputers configureren met het bewerken van het bestand oidc_clientconf.xml</span><span class="sxs-lookup"><span data-stu-id="38e70-163">Configure your client by editing the oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="38e70-164">Omdat u van OAuth2-stromen gebruikmaakt alleen voor een token verkrijgen en de Graph-API aanroepen, moet u de client te doen OAuth2 alleen instellen.</span><span class="sxs-lookup"><span data-stu-id="38e70-164">Because you are using OAuth2 flows only to get a token and call the Graph API, set the client to do OAuth2 only.</span></span> <span data-ttu-id="38e70-165">OIDC wordt geleverd in een voorbeeld van een hoger.</span><span class="sxs-lookup"><span data-stu-id="38e70-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="38e70-166">Configureer uw client-ID die u hebt ontvangen van de portal voor wachtwoordregistratie.</span><span class="sxs-lookup"><span data-stu-id="38e70-166">Configure your client ID that you received from the registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="38e70-167">Configureer uw omleidings-URI met de versie die hieronder.</span><span class="sxs-lookup"><span data-stu-id="38e70-167">Configure your redirect URI with the one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="38e70-168">Configureer uw scopes die u nodig hebt voor toegang tot de Graph API.</span><span class="sxs-lookup"><span data-stu-id="38e70-168">Configure your scopes that you need in order to access the Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="38e70-169">De `User.Read` waarde in `oidc_scopes` kunt u de basisprofiel de ondertekende lezen in het dialoogvenster gebruiker.</span><span class="sxs-lookup"><span data-stu-id="38e70-169">The `User.Read` value in `oidc_scopes` allows you to read the basic profile the signed in user.</span></span>
<span data-ttu-id="38e70-170">U kunt meer informatie over de beschikbare scopes op [Microsoft Graph-machtigingsbereiken](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="38e70-170">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="38e70-171">Als u wilt uitleg over `openid` of `offline_access` als scopes in het OpenID Connect, Zie [2.0-protocollen - stromen van OAuth 2.0 autorisatie Code](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="38e70-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-the-oidcendpointsxml-file"></a><span data-ttu-id="38e70-172">Uw clienteindpunten configureren met het bewerken van het bestand oidc_endpoints.xml</span><span class="sxs-lookup"><span data-stu-id="38e70-172">Configure your client endpoints by editing the oidc_endpoints.xml file</span></span>
* <span data-ttu-id="38e70-173">Open de `oidc_endpoints.xml` -bestand en de volgende wijzigingen aanbrengen:</span><span class="sxs-lookup"><span data-stu-id="38e70-173">Open the `oidc_endpoints.xml` file and make the following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="38e70-174">Deze eindpunten moeten nooit wijzigen als u OAuth2 als protocol gebruikt.</span><span class="sxs-lookup"><span data-stu-id="38e70-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="38e70-175">De eindpunten voor `userInfoEndpoint` en `revocationEndpoint` worden momenteel niet ondersteund door Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="38e70-175">The endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="38e70-176">Als u deze met de standaardwaarde voorbeeld.com laat, wordt u eraan herinnerd dat ze niet beschikbaar in de steekproef zijn :-)</span><span class="sxs-lookup"><span data-stu-id="38e70-176">If you leave these with the default example.com value, you will be reminded that they are not available in the sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="38e70-177">Configureer een Graph API-aanroep</span><span class="sxs-lookup"><span data-stu-id="38e70-177">Configure a Graph API call</span></span>
* <span data-ttu-id="38e70-178">Open de `HomeActivity.java` -bestand en de volgende wijzigingen aanbrengen:</span><span class="sxs-lookup"><span data-stu-id="38e70-178">Open the `HomeActivity.java` file and make the following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="38e70-179">Hier wordt een eenvoudige Graph API-aanroep onze informatie geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="38e70-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="38e70-180">Dit zijn alle wijzigingen die u moet doen.</span><span class="sxs-lookup"><span data-stu-id="38e70-180">Those are all the changes that you need to do.</span></span> <span data-ttu-id="38e70-181">Voer de `oidlib-sample` toepassing en klik op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="38e70-181">Run the `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="38e70-182">Nadat u hebt geverifieerd, selecteert u de **een beveiligde bron aanvragen** knop voor het testen van de aanroep van de Graph API.</span><span class="sxs-lookup"><span data-stu-id="38e70-182">After you've successfully authenticated, select the **Request Protected Resource** button to test your call to the Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="38e70-183">Beveiligingsupdates voor onze product</span><span class="sxs-lookup"><span data-stu-id="38e70-183">Get security updates for our product</span></span>
<span data-ttu-id="38e70-184">We raden u meldingen wilt ontvangen over beveiligingsincidenten in via de [Security TechCenter](https://technet.microsoft.com/security/dd252948) en u te abonneren op Security Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="38e70-184">We encourage you to get notifications about security incidents by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

