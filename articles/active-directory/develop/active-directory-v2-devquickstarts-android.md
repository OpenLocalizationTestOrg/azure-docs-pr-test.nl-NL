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
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>Aanmelden tooan Android-app met behulp van een derde partij-bibliotheek met Graph API met behulp van Hallo v2.0-eindpunt toevoegen
Hallo Microsoft identity-platform gebruikt open standaarden, zoals OAuth2 en OpenID Connect. Ontwikkelaars kunnen een bibliotheek, ze toointegrate met onze services willen gebruiken. ons platform toohelp ontwikkelaars gebruiken met andere bibliotheken, hebben we hoe de enkele scenario's zoals deze één toodemonstrate geschreven tooconfigure van derden bibliotheken tooconnect toohello Microsoft identity-platform. De meeste bibliotheken die implementeren [hello RFC6749 OAuth2-specificatie](https://tools.ietf.org/html/rfc6749) verbinding kunnen maken van toohello Microsoft identity-platform.

Hallo-toepassing die in dit scenario maakt, kunnen gebruikers tootheir organisatie aanmelden en zoekt u naar zichzelf in hun organisatie met behulp van Hallo Graph API.

Als u nieuwe tooOAuth2 of OpenID Connect, kan veel van deze voorbeeldconfiguratie zin tooyou niet maken. Het is raadzaam dat u leest [2.0-protocollen - stromen van OAuth 2.0 autorisatie Code](active-directory-v2-protocols-oauth-code.md) voor de achtergrond.

> [!NOTE]
> Sommige functies van ons platform waarvoor een expressie in Hallo OAuth2 of OpenID Connect standaarden, zoals voorwaardelijke toegang en beheer van Intune vereist u toouse onze open-source bibliotheken voor Microsoft Azure identiteit.
> 
> 

Hallo v2.0-eindpunt biedt geen ondersteuning voor alle Azure Active Directory-scenario's en onderdelen.

> [!NOTE]
> toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).
> 
> 

## <a name="download-hello-code-from-github"></a>Hallo code vanuit GitHub downloaden
Hallo-code voor deze zelfstudie wordt bijgehouden [op GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).  toofollow langs, kunt u [basis van Hallo app downloaden als een ZIP-](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) of kloon Hallo basisproject:

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

U kunt ook gewoon Hallo voorbeeld downloaden en meteen aan de slag:

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a>Een app registreren
Maak een nieuwe app op Hallo [toepassing registratieportal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), of volgen gedetailleerde stappen op Hallo [hoe tooregister een app met Hallo v2.0-eindpunt](active-directory-v2-app-registration.md).  Zorg ervoor dat:

* Kopiëren Hallo **toepassings-Id** die is toegewezen tooyour app omdat u hebt deze snel nodig.
* Hallo toevoegen **Mobile** platform voor uw app.

> Opmerking: Hallo-portal voor registratie van toepassing biedt een **omleidings-URI** waarde. In dit voorbeeld moet u de standaardwaarde Hallo van gebruiken `https://login.microsoftonline.com/common/oauth2/nativeclient`.
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a>Hallo NXOAuth2 van derden bibliotheek downloaden en een werkruimte maken
Voor dit scenario gebruikt u Hallo OIDCAndroidLib vanuit GitHub, namelijk een OAuth2-bibliotheek op basis van Hallo OpenID Connect code van Google. Hallo systeemeigen toepassingsprofiel implementeert en ondersteunt Hallo autorisatie endpoint van Hallo-gebruiker. Dit zijn alles van hello, moet u toointegrate met Hallo Microsoft identiteitsplatform.

Kloon Hallo OIDCAndroidLib opslagplaats tooyour computer.

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a>Uw Android Studio-omgeving instellen
1. Maak een nieuw Android Studio-project en accepteer de standaardinstellingen Hallo in Hallo-wizard.
   
    ![Nieuw project in Android Studio maken](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Doel Android-apparaten](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Een activiteit toomobile toevoegen](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. tooset van uw projectmodules Hallo gekloond opslagplaats toohello projectlocatie verplaatsen. U kunt ook Hallo-project maken en te klonen rechtstreeks toohello projectlocatie.
   
    ![Projectmodules](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. Open Hallo-projectinstellingen modules met behulp van Hallo contextmenu of met behulp van Hallo Ctrl + Alt + rimaire + S snelkoppeling.
   
    ![Modules projectinstellingen](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. Hallo standaard app module verwijderen omdat u wilt dat alleen Hallo container projectinstellingen.
   
    ![Hallo standaard app module](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. Modules importeren vanuit Hallo gekloonde opslagplaats toohello huidige project.
   
    ![Project importeren in gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![nieuwe modulepagina maken](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)
6. Herhaal deze stappen voor Hallo `oidlib-sample` module.
7. Hallo oidclib afhankelijkheden op Hallo controleren `oidlib-sample` module.
   
    ![oidclib afhankelijkheden op Hallo oidlib voorbeeld module](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. Klik op **OK** en wacht tot gradle synchroniseren.
   
    Uw settings.gradle moet eruitzien als:
   
    ![Schermopname van settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. Hallo voorbeeld-app toomake ervoor bouwen dat Hallo voorbeeld juist worden uitgevoerd.
   
    U niet kunt toouse dit met Azure Active Directory nog. Moeten we tooconfigure sommige eindpunten eerst. Dit is tooensure die u hebt geen een problemen Android Studio voordat we Hallo voorbeeld-app aanpassen.
10. Bouwen en uitvoeren van `oidlib-sample` als doel Hallo in Android Studio.
    
    ![Voortgang van de build oidlib-voorbeeld](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. Hallo verwijderen `app ` map die is gegeven wanneer u Hallo module verwijderd uit Hallo project omdat Android Studio niet worden verwijderd voor de veiligheid.
    
    ![Bestandsstructuur met Hallo app-map](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. Open Hallo **configuraties bewerken** menu tooremove Hallo uitvoeren configuratie die ook gegeven is wanneer u Hallo module verwijderd uit het Hallo-project.
    
    ![Configuraties menu Bewerken](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![configuratie van de app uitvoeren](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)

## <a name="configure-hello-endpoints-of-hello-sample"></a>Hallo-eindpunten van Hallo voorbeeld configureren
Nu dat u Hallo hebt `oidlib-sample` met succes is uitgevoerd, bewerk de sommige eindpunten tooget gaan we deze werken met Azure Active Directory.

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a>Configureren van de client door Hallo oidc_clientconf.xml bestand te bewerken
1. Omdat u van OAuth2 stromen alleen tooget een token gebruikmaakt en Hallo Graph API aanroept, stel Hallo client toodo OAuth2 alleen. OIDC wordt geleverd in een voorbeeld van een hoger.
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. Configureer uw client-ID die u hebt ontvangen van Hallo-portal voor wachtwoordregistratie.
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. Configureer uw omleidings-URI Hello een hieronder.
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. Configureer uw scopes die u nodig hebt in volgorde tooaccess Hallo Graph API.
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

Hallo `User.Read` waarde in `oidc_scopes` kunt u tooread Hallo basisprofiel Hallo gebruiker aangemeld.
U kunt meer informatie over alle beschikbare Hallo-scopes op [Microsoft Graph-machtigingsbereiken](https://graph.microsoft.io/docs/authorization/permission_scopes).

Als u wilt uitleg over `openid` of `offline_access` als scopes in het OpenID Connect, Zie [2.0-protocollen - stromen van OAuth 2.0 autorisatie Code](active-directory-v2-protocols-oauth-code.md).

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a>Uw clienteindpunten configureren door Hallo oidc_endpoints.xml bestand te bewerken
* Open Hallo `oidc_endpoints.xml` en breng zo Hallo volgende wijzigingen:
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

Deze eindpunten moeten nooit wijzigen als u OAuth2 als protocol gebruikt.

> [!NOTE]
> Hallo-eindpunten voor `userInfoEndpoint` en `revocationEndpoint` worden momenteel niet ondersteund door Azure Active Directory. Als u deze met de standaardwaarde voorbeeld.com Hallo laat, wordt u eraan herinnerd dat ze niet beschikbaar in de steekproef Hallo zijn :-)
> 
> 

## <a name="configure-a-graph-api-call"></a>Configureer een Graph API-aanroep
* Open Hallo `HomeActivity.java` en breng zo Hallo volgende wijzigingen:
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

Hier wordt een eenvoudige Graph API-aanroep onze informatie geretourneerd.

Alle Hallo wijzigingen dat u toodo moet zijn. Voer Hallo `oidlib-sample` toepassing en klik op **aanmelden**.

Nadat u hebt geverifieerd, selecteert u Hallo **een beveiligde bron aanvragen** knop tootest uw aanroep toohello Graph API.

## <a name="get-security-updates-for-our-product"></a>Beveiligingsupdates voor onze product
We raden u tooget meldingen over beveiligingsincidenten via Hallo [Security TechCenter](https://technet.microsoft.com/security/dd252948) en u te abonneren tooSecurity Advisory Alerts.

