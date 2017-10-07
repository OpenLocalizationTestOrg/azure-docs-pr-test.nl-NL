---
title: 'Azure Active Directory B2C: Voeg Google + als een OAuth2-id-provider met behulp van aangepaste beleid'
description: Voorbeeld met behulp van Google + als id-provider met behulp van OAuth2-protocol
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 4feff21979c9c3b3b12c7a1cae4db0121d1bd79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a>Azure Active Directory B2C: Voeg Google + als een OAuth2-id-provider met behulp van aangepaste beleid

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Deze handleiding laat zien u hoe tooenable aanmelden voor gebruikers van Google + account door gebruik van Hallo [aangepast beleid](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Vereisten

Volledige Hallo stappen voor het Hallo [aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md) artikel.

Deze stappen omvatten:

1.  Maken van een toepassing Google + account.
2.  Hallo Google + account toepassing sleutel tooAzure AD B2C toevoegen
3.  Claims provider tooa beleid toevoegen
4.  Hallo Google + account claims provider tooa gebruiker reis registreren
5.  Uploaden van Hallo beleid tooan Azure AD B2C-tenant en testen

## <a name="create-a-google-account-application"></a>Een toepassing Google + account maken
toouse Google + als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een Google +-toepassing toocreate en leveren met de juiste parameters Hallo. U kunt een Google +-toepassing hier registreren: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)

1.  Ga toohello [Google ontwikkelaars Console](https://console.developers.google.com/) en meld u aan met de referenties van uw Google + account.
2.  Klik op **project maken**, voer een **projectnaam**, en klik vervolgens op **maken**.

3.  Klik op Hallo **menu projecten**.

    ![Google + account - Selecteer project](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  Klik op Hallo  **+**  knop.

    ![Google + rekening - nieuw project maken](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  Voer een **projectnaam**, en klik vervolgens op **maken**.

    ![Google + account - nieuw project](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  Wacht totdat het Hallo-project gereed is en klik op Hallo **menu projecten**.

    ![Wacht totdat de nieuwe project is gereed toouse-Google + account:](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  Klik op de projectnaam van uw.

    ![Google + account - selecteer Hallo nieuw project](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  Klik op **API Manager** en klik vervolgens op **referenties** in Hallo linkernavigatiebalk.
9.  Klik op Hallo **OAuth toestemming scherm** Hallo boven op tabblad.

    ![Google + account - ingesteld OAuth toestemming scherm](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  Selecteer of geef een geldige **e-mailadres**, bieden een **Productnaam**, en klik op **opslaan**.

    ![Google + - toepassing-referenties](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  Klik op **nieuwe referenties** en kies vervolgens **OAuth-Clientidentiteit**.

    ![Google + - referenties van de nieuwe toepassing maken](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  Onder **toepassingstype**, selecteer **webtoepassing**.

    ![Google + - toepassingstype selecteren](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  Geef een **naam** voor uw toepassing, voert u `https://login.microsoftonline.com` in Hallo **geautoriseerd JavaScript oorsprongen** veld en `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in Hallo **geautoriseerde omleidings-URI's**veld. Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com). Hallo **{tenant}** hoofdlettergevoelig. Klik op **Create**.

    ![Google + - JavaScript geautoriseerd oorsprongen bieden en omleidings-URI's](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  Kopieer de waarden Hallo van **Client-Id** en **clientgeheim**. U moet beide tooconfigure Google + als een id-provider in uw tenant. **Clientgeheim** is een belangrijke beveiligingsreferentie.

    ![Google + - kopie Hallo waarden van de client-Id en Client geheim](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a>Hallo Google + account toepassing sleutel tooAzure AD B2C toevoegen
Federatie met Google + accounts vereist een clientgeheim voor Google + account tootrust Azure AD B2C namens Hallo-toepassing. U moet uw Google + toepassingsgeheim in Azure AD B2C-tenant toostore:  

1.  Ga tooyour Azure AD B2C-tenant en selecteer **B2C-instellingen** > **identiteit ervaring Framework**
2.  Selecteer **beleid sleutels** tooview Hallo sleutels die beschikbaar zijn in uw tenant.
3.  Klik op **+ toevoegen**.
4.  Voor **opties**, gebruik **handmatige**.
5.  Voor **naam**, gebruik `GoogleSecret`.  
    Hallo voorvoegsel `B2C_1A_` kunnen automatisch worden toegevoegd.
6.  In Hallo **geheim** Voer uw Microsoft-toepassingsgeheim van https://apps.dev.microsoft.com
7.  Voor **sleutelgebruik**, gebruik **handtekening**.
8.  Klik op **Maken**.
9.  Bevestig dat u hebt gemaakt dat Hallo sleutel `B2C_1A_GoogleSecret`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Toevoegen van een claimprovider in de uitbreiding beleid

Als u wilt dat gebruikers toosign in met behulp van Google + account, moet u toodefine Google + account als een claimprovider. Met andere woorden, moet u een eindpunt dat Azure AD B2C met communiceert toospecify. Hallo-eindpunt biedt een set claims die worden gebruikt door Azure AD B2C-tooverify die een specifieke gebruiker is geverifieerd.

Google + Account definiëren als een claimprovider door toe te voegen `<ClaimsProvider>` knooppunt in het beleidsbestand extensie:

1.  Bestand met beleidsregel van Hallo-extensie (TrustFrameworkExtensions.xml) openen vanuit uw werkmap. Als u een XML-editor moet [Visual Studio Code probeert](https://code.visualstudio.com/download), een lichtgewicht platformoverschrijdende-editor.
2.  Hallo zoeken `<ClaimsProviders>` sectie
3.  Toevoegen van de volgende XML-fragment onder Hallo Hallo `ClaimsProviders` element en vervang `client_id` waarde met uw Google + account toepassing client-ID vóór Hallo-bestand op te slaan.  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want hello user tooselect his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Hallo Google + account claims provider tooSign up registreren of aanmelden gebruiker reis

Hallo-id-provider is ingesteld.  Het is echter niet beschikbaar in een van de Hallo sign-up-to-date/aanmelden schermen. Hallo Google + account-id-provider tooyour gebruiker toevoegen `SignUpOrSignIn` traject van de gebruiker. toomake deze beschikbaar, maken we een duplicaat van een bestaande sjabloon gebruiker reis.  Vervolgens toevoegen we Hallo Google + account id-provider:

>[!NOTE]
>
>Als u Hallo gekopieerd `<UserJourneys>` element uit de base-bestand van uw beleid toohello extensiebestand (TrustFrameworkExtensions.xml), kunt u toothis sectie overslaan.

1.  Open base Hallo-bestand van uw beleid (bijvoorbeeld TrustFrameworkBase.xml).
2.  Hallo zoeken `<UserJourneys>` element en kopieer Hallo volledige inhoud van `<UserJourneys>` knooppunt.
3.  Hallo-extensiebestand (bijvoorbeeld TrustFrameworkExtensions.xml) openen en zoeken van Hallo `<UserJourneys>` element. Als Hallo element niet bestaat, Voeg een.
4.  Hallo volledige inhoud van plakken `<UserJournesy>` knooppunt dat u hebt gekopieerd als een onderliggend element van Hallo `<UserJourneys>` element.

### <a name="display-hello-button"></a>Hallo-knop weergave
Hallo `<ClaimsProviderSelections>` element Hallo lijst met opties voor de selectie van claims provider en de volgorde gedefinieerd.  `<ClaimsProviderSelection>`element is vergelijkbaar tooan identiteit provider knop op een pagina sign-up-to-date/aanmelden. Als u een `<ClaimsProviderSelection>` element voor Google + account, een nieuwe knop wordt weergegeven wanneer een gebruiker op de pagina Hallo terechtkomt. tooadd dit element:

1.  Hallo zoeken `<UserJourney>` knooppunt met `Id="SignUpOrSignIn"` in Hallo gebruiker reis die u hebt gekopieerd.
2.  Zoek Hallo `<OrchestrationStep>` knooppunt bevat`Order="1"`
3.  Plaats de volgende XML-fragment onder `<ClaimsProviderSelections>` knooppunt:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Koppeling Hallo knop tooan actie
Nu u een knop hebt geïmplementeerd, moet u toolink het tooan in te grijpen. Hallo-actie is in dit geval voor Azure AD B2C toocommunicate met Google + account tooreceive een token.

1.  Hallo zoeken `<OrchestrationStep>` die omvat `Order="2"` in Hallo `<UserJourney>` knooppunt.
2.  Plaats de volgende XML-fragment onder `<ClaimsExchanges>` knooppunt:

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * Zorg ervoor dat Hallo `Id` heeft dezelfde als die van waarde Hallo `TargetClaimsExchangeId` in de voorgaande sectie Hallo
> * Zorg ervoor dat `TechnicalProfileReferenceId` ID toohello technische profiel gemaakt van eerdere (Google OAUTH) is ingesteld.

## <a name="upload-hello-policy-tooyour-tenant"></a>Hallo beleid tooyour tenant uploaden
1.  In Hallo [Azure-portal](https://portal.azure.com), schakel over naar Hallo [context van uw Azure AD B2C-tenant](active-directory-b2c-navigate-to-b2c-context.md), en open Hallo **Azure AD B2C** blade.
2.  Selecteer **identiteit ervaring Framework**.
3.  Open Hallo **alle beleidsregels** blade.
4.  Selecteer **uploaden beleid**.
5.  Controleer **Hallo beleid overschreven als deze bestaat** vak.
6.  **Uploaden** TrustFrameworkExtensions.xml en zorg ervoor dat deze niet Hallo validatie mislukt

## <a name="test-hello-custom-policy-by-using-run-now"></a>Hallo aangepast beleid testen met behulp van nu uitvoeren
1.  Open **Azure AD B2C-instellingen** en ga te**identiteit ervaring Framework**.

    >[!NOTE]
    >
    >    **Nu uitvoeren** vereist ten minste één toepassing toobe preregistered op Hallo-tenant. 
    >    hoe tooregister toepassingen, Zie toolearn hello Azure AD B2C [aan de slag](active-directory-b2c-get-started.md) artikel of Hallo [toepassingsregistratie](active-directory-b2c-app-registration.md) artikel.


2.  Open **B2C_1A_signup_signin**, Hallo relying party (RP) aangepast beleid dat u hebt geüpload. Selecteer **nu uitvoeren**.
3.  U moet kunnen toosign met Google + account.

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a>[Optioneel] Hallo Google + account claims provider tooProfile bewerken gebruiker reis registreren
U kunt aangeven tooadd Hallo Google + account identiteitsprovider ook tooyour gebruiker `ProfileEdit` traject van de gebruiker. toomake deze beschikbaar zijn, herhaalt u Hallo laatste twee stappen:

### <a name="display-hello-button"></a>Hallo-knop weergave
1.  Open de extensiebestand Hallo van uw beleid (bijvoorbeeld TrustFrameworkExtensions.xml).
2.  Hallo zoeken `<UserJourney>` knooppunt met `Id="ProfileEdit"` in Hallo gebruiker reis die u hebt gekopieerd.
3.  Zoek Hallo `<OrchestrationStep>` knooppunt bevat`Order="1"`
4.  Plaats de volgende XML-fragment onder `<ClaimsProviderSelections>` knooppunt:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Koppeling Hallo knop tooan actie
1.  Hallo zoeken `<OrchestrationStep>` die omvat `Order="2"` in Hallo `<UserJourney>` knooppunt.
2.  Plaats de volgende XML-fragment onder `<ClaimsExchanges>` knooppunt:

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Hallo aangepast profiel bewerken beleid testen met behulp van nu uitvoeren

1.  Open **Azure AD B2C-instellingen** en ga te**identiteit ervaring Framework**.
2.  Open **B2C_1A_ProfileEdit**, Hallo relying party (RP) aangepast beleid dat u hebt geüpload. Selecteer **nu uitvoeren**.
3.  U moet kunnen toosign met Google + account.

## <a name="download-hello-complete-policy-files"></a>Downloaden voltooid Hallo-beleidsbestanden
Optioneel: We raden aan bouwen van uw scenario met behulp van uw eigen aangepaste beleidsbestanden na het voltooien van Hallo in plaats van deze voorbeeldbestanden aan de slag met aangepast beleid dat is doorlopen.  [Beleid voorbeeldbestanden voor verwijzing](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
