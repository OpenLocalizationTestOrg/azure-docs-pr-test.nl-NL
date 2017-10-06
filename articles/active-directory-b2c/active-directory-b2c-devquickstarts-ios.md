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
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a>Azure AD B2C: Meld u aan met een iOS-toepassing

Hallo Microsoft identity-platform gebruikt open standaarden, zoals OAuth2 en OpenID Connect. Gebruik van een open standaard protocol biedt meer mogelijkheden voor ontwikkelaars bij het selecteren van een bibliotheek toointegrate met onze services. We bieden in dit scenario en andere leuk tooaid ontwikkelaars met het schrijven van toepassingen die verbinding toohello Microsoft Identity-platform maken. De meeste bibliotheken die implementeren [hello RFC6749 OAuth2-specificatie](https://tools.ietf.org/html/rfc6749) zijn kunnen tooconnect toohello Microsoft Identity-platform.

> [!WARNING]
> Microsoft biedt geen oplossingen voor de bibliotheken van derden en een overzicht van deze bibliotheken niet uitgevoerd. Dit voorbeeld maakt gebruik van een derde partij bibliotheek aangeroepen AppAuth dat is getest op compatibiliteit in algemene scenario's met hello Azure AD B2C. Problemen en functie-aanvragen moeten gerichte toohello-bibliotheek open source-project. Raadpleeg [dit artikel](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) voor meer informatie.
>
>

Als u nieuwe tooOAuth2 of OpenID Connect, kan veel van deze voorbeeldconfiguratie veel tooyou zin niet maken. We raden u een korte bekijkt [overzicht van het Hallo-protocol we hier hebt gedocumenteerd](active-directory-b2c-reference-protocols.md).

## <a name="get-an-azure-ad-b2c-directory"></a>Een Azure AD B2C-directory maken
Voordat u Azure AD B2C kunt gebruiken, moet u een directory, of tenant, maken. Een directory is een container voor alle gebruikers, apps en groepen. Als u nog geen directory hebt, [maakt u een B2C-directory](active-directory-b2c-get-started.md) voordat u verdergaat.

## <a name="create-an-application"></a>Een app maken
Vervolgens moet u een app toocreate in uw B2C-directory. Hallo app-registratie biedt informatie over het Azure AD dat het moet toocommunicate veilig met uw app. Volg toocreate een mobiele app [deze instructies](active-directory-b2c-app-registration.md). Zorg ervoor dat:

* Omvatten een **Native client** in Hallo-toepassing.
* Kopiëren Hallo **toepassings-ID** is toegewezen tooyour app. U hebt deze GUID later nodig.
* Instellen van een **omleidings-URI** met een aangepast schema (bijvoorbeeld com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect). U hebt deze URI later nodig.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Het beleid maken
In Azure AD B2C wordt elke gebruikerservaring gedefinieerd door [beleid](active-directory-b2c-reference-policies.md). Deze app bevat één identiteit ervaring: een gecombineerde aanmelden en registreren. Maak van dit beleid, zoals beschreven in de [naslagartikel](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Wanneer u Hallo beleid maakt, moet u:

* Onder **registratiekenmerken**, selecteer Hallo kenmerk **weergavenaam**.  U kunt ook andere kenmerken selecteren.
* Onder **toepassingsclaims**, selecteert u de claims Hallo **weergavenaam** en **Object-ID van gebruiker**. U kunt ook andere claims selecteren.
* Kopiëren Hallo **naam** van elk beleid nadat u dit hebt gemaakt. De beleidsnaam van uw wordt voorafgegaan door `b2c_1_` wanneer u Hallo beleid opslaat.  U nodig beleidsnaam hello later.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Wanneer u uw beleid hebt gemaakt, bent u klaar toobuild uw app.

## <a name="download-hello-sample-code"></a>Hallo voorbeeldcode downloaden
We hebben een werkende-voorbeeldtoepassing die gebruikmaakt van AppAuth met Azure AD B2C opgegeven [op GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c). U kunt downloaden Hallo code en voer deze uit. toouse uw eigen Azure AD B2C-tenant, volg de instructies Hallo in Hallo [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).

Dit voorbeeld is gemaakt door Hallo Leesmij-instructies te volgen door Hallo [AppAuth iOS-project op GitHub](https://github.com/openid/AppAuth-iOS). Voor meer informatie over de werking van Hallo-bibliotheek en Hallo voorbeelden Hallo verwijzing AppAuth README op GitHub.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Uw app toouse Azure AD B2C met AppAuth wijzigen

> [!NOTE]
> AppAuth biedt ondersteuning voor iOS 7 en hoger.  Sociale aanmeldingen op Google, SFSafariViewController toosupport is echter waarvoor iOS 9 of hoger vereist.
>

### <a name="configuration"></a>Configuratie

U kunt de communicatie met Azure AD B2C configureren door te geven zowel Hallo autorisatie eindpunt en token eindpunt URI's.  toogenerate deze URI's, moet u Hallo volgende informatie:
* Tenant-ID (bijvoorbeeld: contoso.onmicrosoft.com)
* De naam van beleid (bijvoorbeeld B2C\_1\_SignUpIn)

Hallo-tokeneindpunt URI kan worden gegenereerd door te vervangen Hallo Tenant\_-ID en het Hallo beleid\_naam in Hallo URL te volgen:

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

Hallo autorisatie eindpunt URI kan worden gegenereerd door te vervangen Hallo Tenant\_-ID en het Hallo beleid\_naam in Hallo URL te volgen:

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

Voer Hallo code toocreate na uw AuthorizationServiceConfiguration-object:

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a>Autoriseren

Na het configureren van of bij het ophalen van een configuratie van de service autorisatie, kan een autorisatieaanvraag worden samengesteld. Hallo toocreate aanvragen, moet u de volgende informatie Hallo:  
* Client-ID (bijvoorbeeld 00000000-0000-0000-0000-000000000000)
* Omleidings-URI met een aangepast schema (bijvoorbeeld com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)

Beide items moeten zijn opgeslagen als u zijn [u uw app registreert](#create-an-application).

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

tooset van uw toepassing toohandle Hallo omleiding toohello URI met het aangepaste schema hello, moet u tooupdate Hallo lijst met URL-schema in uw Info.pList:
* Open Info.pList.
* Beweeg de muisaanwijzer over een rij zoals bundel OS typecode en klikt u op Hallo \+ symbool.
* Wijzig de naam Hallo nieuwe rij 'URL typen'.
* Klik op Hallo pijl toohello links van URL-types tooopen Hallo structuur.
* Klik op Hallo pijl toohello links van '0-Item' tooopen Hallo structuur.
* Wijzig de naam van eerste item onder Item 0 too'URL regelingen.
* Klik op Hallo pijl toohello links van URL-schema tooopen Hallo structuur.
* In de kolom 'Waarde' hello, is een leeg veld toohello links van '0 Item' onder de URL-schema.  De unieke schema Hallo waarde tooyour van de toepassing ingesteld.  Hallo-waarde moet overeenkomen met de Hallo dat wordt gebruikt in URL omleiding wanneer u Hallo OIDAuthorizationRequest object maakt.  In ons voorbeeld hebben we com.onmicrosoft.fabrikamb2c.exampleapp' hello schema' gebruikt.

Raadpleeg toohello [AppAuth handleiding](https://openid.github.io/AppAuth-iOS/) op hoe toocomplete Hallo rest van het Hallo-proces. Als u tooquickly moet aan de slag met een app werken, Bekijk [ons voorbeeld](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c). Volg de stappen Hallo in Hallo [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter uw eigen Azure AD B2C-configuratie.

We zijn altijd open toofeedback en suggesties! Als u problemen met dit onderwerp ondervindt of aanbevelingen voor het verbeteren van de inhoud hebben, zou wij stellen uw feedback Hallo Hallo pagina onderaan in. Voor functieaanvragen, toe te voegen te[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).
