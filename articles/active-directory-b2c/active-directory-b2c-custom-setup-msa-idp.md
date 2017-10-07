---
title: 'Azure Active Directory B2C: Microsoft-Account (MSA) toevoegen als een id-provider met behulp van aangepaste beleid'
description: Voorbeeld met behulp van Microsoft als id-provider met OpenID Connect (OIDC)-protocol
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
ms.openlocfilehash: 577ac612f69015e6790f2fa9f2cfb42c2b524b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a>Azure Active Directory B2C: Microsoft-Account (MSA) toevoegen als een id-provider met behulp van aangepaste beleid

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Dit artikel ziet u hoe tooenable aanmelden voor gebruikers van Microsoft-account (MSA) door het gebruik van Hallo [aangepast beleid](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Vereisten
Volledige Hallo stappen voor het Hallo [aan de slag met aangepaste beleidsregels](active-directory-b2c-get-started-custom.md) artikel.

Deze stappen omvatten:

1.  Maken van een toepassing van Microsoft-account.
2.  Hallo Microsoft-account toepassing sleutel tooAzure AD B2C toevoegen
3.  Claims provider tooa beleid toevoegen
4.  Hallo Microsoft-Account claims provider tooa gebruiker reis registreren
5.  Uploaden van Hallo beleid tooan Azure AD B2C-tenant en testen

## <a name="create-a-microsoft-account-application"></a>Een toepassing van Microsoft-account maken
toouse Microsoft account toe als een id-provider in Azure Active Directory (Azure AD) B2C, u moet een Microsoft-account-toepassing toocreate en leveren met de juiste parameters Hallo. U moet een Microsoft-account. Als u niet hebt, gaat u naar [https://www.live.com/](https://www.live.com/).

1.  Ga toohello [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) en meld u aan met uw Microsoft-accountreferenties.
2.  Klik op **een app toevoegen**.

    ![Microsoft-account: een app toevoegen](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  Bieden een **naam** voor uw toepassing **Neem contact op met de e-mailadres**, schakel het selectievakje **wij kunnen u helpen** en klik op **maken**.

    ![Microsoft-account - uw toepassing registreren](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  Hallo-waarde van kopiëren **toepassings-Id**. U moet deze tooconfigure Microsoft-account als een id-provider in uw tenant.

    ![Microsoft-account - waarde van de kopie Hallo van toepassings-Id](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  Klik op **platform toevoegen**

    ![Microsoft-account - platform toevoegen](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  Kies in de lijst met platforms van hello, **Web**.

    ![Microsoft-account - Kies in de lijst met Hallo-platforms Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  Voer `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in Hallo **omleidings-URI's** veld. Vervang **{tenant}** met de naam van uw tenant (bijvoorbeeld contosob2c.onmicrosoft.com).

    ![Microsoft-account - Set Omleidings-URL 's](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  Klik op **nieuw wachtwoord genereren** onder Hallo **toepassing geheimen** sectie. Kopieer Hallo nieuw wachtwoord op het scherm wordt weergegeven. U moet deze tooconfigure Microsoft-account als een id-provider in uw tenant. Dit wachtwoord is een belangrijke beveiligingsreferentie.

    ![Microsoft-account: nieuw wachtwoord genereren](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Microsoft-account - kopie Hallo nieuw wachtwoord](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  Selectievakje Hallo waarin staat dat **ondersteuning voor Live SDK** onder Hallo **geavanceerde opties** sectie. Klik op **Opslaan**.

    ![Microsoft-account - ondersteuning voor Live SDK](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a>Hallo Microsoft-account toepassing sleutel tooAzure AD B2C toevoegen
Federatie met Microsoft-accounts vereist een clientgeheim voor Microsoft-account tootrust Azure AD B2C namens Hallo-toepassing. U moet uw Microsoft-account toepassing secert in Azure AD B2C-tenant toostore:   

1.  Ga tooyour Azure AD B2C-tenant en selecteer **B2C-instellingen** > **identiteit ervaring Framework**
2.  Selecteer **beleid sleutels** tooview Hallo sleutels die beschikbaar zijn in uw tenant.
3.  Klik op **+ toevoegen**.
4.  Voor **opties**, gebruik **handmatige**.
5.  Voor **naam**, gebruik `MSASecret`.  
    Hallo voorvoegsel `B2C_1A_` kunnen automatisch worden toegevoegd.
6.  In Hallo **geheim** Voer uw Microsoft-toepassingsgeheim van https://apps.dev.microsoft.com
7.  Voor **sleutelgebruik**, gebruik **handtekening**.
8.  Klik op **Maken**.
9.  Bevestig dat u hebt gemaakt dat Hallo sleutel `B2C_1A_MSASecret`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Toevoegen van een claimprovider in de uitbreiding beleid
Als u wilt dat gebruikers toosign in met behulp van Microsoft-Account, moet u toodefine Microsoft-Account als een claimprovider. Met andere woorden, moet u een eindpunt dat Azure AD B2C met communiceert toospecify. Hallo-eindpunt biedt een set claims die worden gebruikt door Azure AD B2C-tooverify die een specifieke gebruiker is geverifieerd.

Microsoft-Account definiëren als een claimprovider door toe te voegen `<ClaimsProvider>` knooppunt in het beleidsbestand extensie:

1.  Bestand met beleidsregel van Hallo-extensie (TrustFrameworkExtensions.xml) openen vanuit uw werkmap. Als u een XML-editor moet [Visual Studio Code probeert](https://code.visualstudio.com/download), een lichtgewicht platformoverschrijdende-editor.
2.  Hallo zoeken `<ClaimsProviders>` sectie
3.  Plaats de volgende XML-fragment onder Hallo `ClaimsProviders` element:

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

4.  Vervang `client_id` waarde met uw client-Id van de toepassing in Microsoft-Account

5.  Hallo-bestand opslaan.

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Hallo Microsoft-Account claims provider tooSign omhoog of reis aanmelden gebruiker registreren

Op dit moment Hallo id-provider is ingesteld, maar het is niet beschikbaar is in geen van Hallo sign-up-to-date/aanmelden schermen. Nu u tooadd Hallo Microsoft-Account-id-provider tooyour gebruiker moet `SignUpOrSignIn` traject van de gebruiker. toomake deze beschikbaar, maken we een duplicaat van een bestaande sjabloon gebruiker reis.  Vervolgens toevoegen we Hallo Microsoft-Account-id-provider:

> [!NOTE]
>
>Als u eerder hebt gekopieerd in Hallo `<UserJourneys>` element uit de base-bestand van uw beleid toohello-extensiebestand `TrustFrameworkExtensions.xml`, kunt u toothis sectie overslaan.

1.  Open base Hallo-bestand van uw beleid (bijvoorbeeld TrustFrameworkBase.xml).
2.  Hallo zoeken `<UserJourneys>` element en kopieer Hallo volledige inhoud van `<UserJourneys>` knooppunt.
3.  Hallo-extensiebestand (bijvoorbeeld TrustFrameworkExtensions.xml) openen en zoeken van Hallo `<UserJourneys>` element. Als Hallo element niet bestaat, Voeg een.
4.  Hallo volledige inhoud van plakken `<UserJournesy>` knooppunt dat u hebt gekopieerd als een onderliggend element van Hallo `<UserJourneys>` element.

### <a name="display-hello-button"></a>Hallo-knop weergave
Hallo `<ClaimsProviderSelections>` element Hallo lijst met opties voor de selectie van claims provider en de volgorde gedefinieerd.  `<ClaimsProviderSelection>`element is vergelijkbaar tooan identiteit provider knop op een pagina sign-up-to-date/aanmelden. Als u een `<ClaimsProviderSelection>` element voor Microsoft-account, een nieuwe knop wordt weergegeven wanneer een gebruiker op de pagina Hallo terechtkomt. tooadd dit element:

1.  Hallo zoeken `<UserJourney>` knooppunt met `Id="SignUpOrSignIn"` in Hallo gebruiker reis die u hebt gekopieerd.
2.  Zoek Hallo `<OrchestrationStep>` knooppunt bevat`Order="1"`
3.  Plaats de volgende XML-fragment onder `<ClaimsProviderSelections>` knooppunt:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Koppeling Hallo knop tooan actie
Nu u een knop hebt geïmplementeerd, moet u toolink het tooan in te grijpen. Hallo-actie is in dit geval voor Azure AD B2C toocommunicate met Microsoft-Account tooreceive een token. Hallo knop tooan actie door te koppelen van technische Hallo-profiel voor de claimprovider van uw Microsoft-Account koppelen:

1.  Hallo zoeken `<OrchestrationStep>` die omvat `Order="2"` in Hallo `<UserJourney>` knooppunt.
2.  Plaats de volgende XML-fragment onder `<ClaimsExchanges>` knooppunt:

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * Zorg ervoor dat Hallo `Id` heeft dezelfde als die van waarde Hallo `TargetClaimsExchangeId` in de voorgaande sectie Hallo
>   * Zorg ervoor dat `TechnicalProfileReferenceId` ID toohello technische profiel gemaakt van eerdere (MSA OIDC) is ingesteld.

## <a name="upload-hello-policy-tooyour-tenant"></a>Hallo beleid tooyour tenant uploaden
1.  In Hallo [Azure-portal](https://portal.azure.com), schakel over naar Hallo [context van uw Azure AD B2C-tenant](active-directory-b2c-navigate-to-b2c-context.md), en open Hallo **Azure AD B2C** blade.
2.  Selecteer **identiteit ervaring Framework**.
3.  Open Hallo **alle beleidsregels** blade.
4.  Selecteer **uploaden beleid**.
5.  Controleer **Hallo beleid overschreven als deze bestaat** vak.
6.  **Uploaden** TrustFrameworkExtensions.xml en zorg ervoor dat deze niet Hallo validatie mislukt

## <a name="test-hello-custom-policy-by-using-run-now"></a>Hallo aangepast beleid testen met behulp van nu uitvoeren

1.  Open **Azure AD B2C-instellingen** en ga te**identiteit ervaring Framework**.
> [!NOTE]
>
>**Nu uitvoeren** vereist ten minste één toepassing toobe preregistered op Hallo-tenant. hoe tooregister toepassingen, Zie toolearn hello Azure AD B2C [aan de slag](active-directory-b2c-get-started.md) artikel of Hallo [toepassingsregistratie](active-directory-b2c-app-registration.md) artikel.
2.  Open **B2C_1A_signup_signin**, Hallo relying party (RP) aangepast beleid dat u hebt geüpload. Selecteer **nu uitvoeren**.
3.  U moet kunnen toosign met Microsoft-account.

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a>[Optioneel] Hallo Microsoft-Account claims provider tooProfile bewerken gebruiker reis registreren
U kunt aangeven tooadd Hallo Microsoft-Account-id-provider ook tooyour gebruiker `ProfileEdit` traject van de gebruiker. toomake deze beschikbaar zijn, herhaalt u Hallo laatste twee stappen:

### <a name="display-hello-button"></a>Hallo-knop weergave
1.  Open de extensiebestand Hallo van uw beleid (bijvoorbeeld TrustFrameworkExtensions.xml).
2.  Hallo zoeken `<UserJourney>` knooppunt met `Id="ProfileEdit"` in Hallo gebruiker reis die u hebt gekopieerd.
3.  Zoek Hallo `<OrchestrationStep>` knooppunt bevat`Order="1"`
4.  Plaats de volgende XML-fragment onder `<ClaimsProviderSelections>` knooppunt:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Koppeling Hallo knop tooan actie
1.  Hallo zoeken `<OrchestrationStep>` die omvat `Order="2"` in Hallo `<UserJourney>` knooppunt.
2.  Plaats de volgende XML-fragment onder `<ClaimsExchanges>` knooppunt:

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Hallo aangepast profiel bewerken beleid testen met behulp van nu uitvoeren
1.  Open **Azure AD B2C-instellingen** en ga te**identiteit ervaring Framework**.
2.  Open **B2C_1A_ProfileEdit**, Hallo relying party (RP) aangepast beleid dat u hebt geüpload. Selecteer **nu uitvoeren**.
3.  U moet kunnen toosign met Microsoft-account.

## <a name="download-hello-complete-policy-files"></a>Downloaden voltooid Hallo-beleidsbestanden
Optioneel: We raden aan bouwen van uw scenario met behulp van uw eigen aangepaste beleidsbestanden na het voltooien van Hallo in plaats van deze voorbeeldbestanden aan de slag met aangepast beleid dat is doorlopen.  [Beleid voorbeeldbestanden voor verwijzing](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
