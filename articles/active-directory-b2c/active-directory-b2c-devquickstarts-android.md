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
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a>Azure AD B2C: Meld u aan met een Android-toepassing

Hallo Microsoft identity-platform gebruikt open standaarden, zoals OAuth2 en OpenID Connect. Hierdoor kunnen ontwikkelaars tooleverage een bibliotheek, willen ze toointegrate met onze services. tooaid ontwikkelaars bij het gebruik van ons platform met andere bibliotheken, we geschreven enkele scenario's zoals deze één toodemonstrate hoe tooconfigure 3e partij bibliotheken tooconnect toohello Microsoft identity-platform. De meeste bibliotheken die implementeren [hello RFC6749 OAuth2-specificatie](https://tools.ietf.org/html/rfc6749) worden kunnen tooconnect toohello Microsoft Identity-platform.

> [!WARNING]
> Microsoft biedt geen oplossingen voor 3rd partij bibliotheken en een overzicht van deze bibliotheken niet uitgevoerd. Dit voorbeeld maakt gebruik van een 3e partij-bibliotheek AppAuth dat is getest op compatibiliteit in algemene scenario's met hello Azure AD B2C. Problemen en functie-aanvragen moeten gerichte toohello-bibliotheek open source-project. Zie [in dit artikel](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) voor meer informatie.  
>
>

Als u nieuwe tooOAuth2 of OpenID Connect mogelijk veel van deze voorbeeldconfiguratie veel tooyou zin niet maken. We raden u een korte bekijkt [overzicht van het Hallo-protocol we hier hebt gedocumenteerd](active-directory-b2c-reference-protocols.md).

## <a name="get-an-azure-ad-b2c-directory"></a>Een Azure AD B2C-directory maken

Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken. Een directory is een container voor alle gebruikers, apps, groepen en meer. Als u nog geen directory hebt, [maakt u een B2C-directory](active-directory-b2c-get-started.md) voordat u verdergaat.

## <a name="create-an-application"></a>Een app maken

Vervolgens moet u een app toocreate in uw B2C-directory. Hiermee geeft u Azure AD-informatie dat het moet toocommunicate veilig met uw app. Volg toocreate een mobiele app [deze instructies](active-directory-b2c-app-registration.md). Zorg ervoor dat:

* Omvatten een **Native Client** in Hallo-toepassing.
* Kopiëren Hallo **toepassings-ID** is toegewezen tooyour app. U nodig deze later.
* Instellen van een native client **omleidings-URI** (bijvoorbeeld com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect). Deze hebt u ook later nodig.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Het beleid maken

In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md). Deze app bevat één identiteit ervaring: een gecombineerde aanmelden en registreren. U moet toocreate dit beleid, zoals beschreven in de [naslagartikel](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Wanneer u Hallo beleid maakt, moet u:

* Kies Hallo **weergavenaam** als een kenmerk aanmelding in uw beleid.
* Kies Hallo **weergavenaam** en **Object-ID** toepassingsclaims voor elk beleid. U kunt ook andere claims kiezen.
* Kopiëren Hallo **naam** van elk beleid nadat u dit hebt gemaakt. Het voorvoegsel Hallo heeft `b2c_1_`.  U hebt de beleidsnaam hello later nodig.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Wanneer u uw beleid hebt gemaakt, bent u klaar toobuild uw app.

## <a name="download-hello-sample-code"></a>Hallo voorbeeldcode downloaden

We hebben een werkende-voorbeeldtoepassing die gebruikmaakt van AppAuth met Azure AD B2C opgegeven [op GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c). U kunt downloaden Hallo code en voer deze uit. U kunt snel aan de slag met uw eigen app met behulp van uw eigen Azure AD B2C-configuratie door de instructies te volgen Hallo in Hallo [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).

Hallo-voorbeeld is een wijziging van Hallo voorbeeld dat is opgegeven door [AppAuth](https://openid.github.io/AppAuth-Android/). Ga naar de pagina toolearn meer over AppAuth en de bijbehorende functies.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Uw app toouse Azure AD B2C met AppAuth wijzigen

> [!NOTE]
> AppAuth biedt ondersteuning voor Android-API 16 (Jellybean) en hoger. Het is raadzaam met behulp van API 23 en hoger.
>

### <a name="configuration"></a>Configuratie

U kunt de communicatie met Azure AD B2C configureren waarmee Hallo detecteren URI of door te geven zowel Hallo autorisatie eindpunt en token eindpunt URI's. In beide gevallen moet u Hallo volgende informatie:

* Tenant-ID (bijvoorbeeld contoso.onmicrosoft.com)
* De naam van beleid (bijvoorbeeld B2C\_1\_SignUpIn)

Als u ervoor kiezen tooautomatically Hallo autorisatie en token-eindpunt URI's detecteren, moet u toofetch informatie van Hallo detectie URI. Hallo detectie URI kan worden gegenereerd door de Hallo Tenant\_-ID en het Hallo beleid\_naam in Hallo URL te volgen:

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

U kunt verkrijgen Hallo autorisatie en -tokeneindpunt URI's en maken van een object AuthorizationServiceConfiguration door Hallo volgende:

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

In plaats van detectie tooobtain Hallo autorisatie en -tokeneindpunt URI's gebruikt, kunt u ook opgeven ze expliciet door te vervangen Hallo Tenant\_-ID en het Hallo beleid\_hieronder de naam in Hallo-URL:

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

Voer Hallo code toocreate na uw AuthorizationServiceConfiguration-object:

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a>Autoriseren

Na het configureren van of bij het ophalen van een configuratie van de service autorisatie, kan een autorisatieaanvraag worden samengesteld. Hallo toocreate aanvragen, moet u Hallo volgende informatie:

* Client-ID (bijvoorbeeld 00000000-0000-0000-0000-000000000000)
* Omleidings-URI met een aangepast schema (bijvoorbeeld com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)

Beide items moeten zijn opgeslagen als u zijn [u uw app registreert](#create-an-application).

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

Raadpleeg toohello [AppAuth handleiding](https://openid.github.io/AppAuth-Android/) op hoe toocomplete Hallo rest van het Hallo-proces. Als u tooquickly moet aan de slag met een app werken, Bekijk [ons voorbeeld](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c). Volg de stappen Hallo in Hallo [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter uw eigen Azure AD B2C-configuratie.

We zijn altijd open toofeedback en suggesties! Als u problemen met dit onderwerp ondervindt of aanbevelingen voor het verbeteren van de inhoud hebben, zou wij stellen uw feedback Hallo Hallo pagina onderaan in. Voor functieaanvragen, toe te voegen te[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).

